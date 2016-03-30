---
layout:     post
title:      "vfs"
subtitle:   " \"vfs\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
VFS
-----------------------------------------------------------------------
sys_read
	current->file->f_op->read();


超级块对象
-------------------------------------------------
struct supper_block
{
	struct list_head 	s_list;		//把supper_block连接在一起,全局super_blocks
	kdev_t			s_dev;
	struct list_head	s_dirty;	//脏inode节点, link by inode->i_list
}



索引节点对象
------------------------------------------------
struct inode
{
	struct list_head	i_hash;
	struct list_head	i_list;		//放在全局列表中
	struct list_head	i_dentry;	//每个inode可能存在多个目录项
}
索引节点对文件是唯一的，随文件存在而存在。


全局列表	//link by inode->i_list
inode_in_use	//inode.i_count > 0; 页面不脏;的inode存在于这个列表中
inode_unused	//inode.i_count - 0; 页面不脏;的inode存在于这个列表中
anon_hash_chain	//inodes with NULL i_sb;
sb->i_dirty	//脏inode

全局hash表
static struct list_head *inode_hashtable;//inode->i_hash解决hash冲突



file对象
-------------------------------------------------------
描述进程怎样与打开的文件交互，文件对象爱你个在文件被打开时创建
struct file
{
	struct list_head	f_list;
	sturct dentry*		f_dentry;
	struct vfsmount*	f_vfsmnt;
	struct file_operations*	f_op;
	unsigned int 		f_count;	//引用计数
}

全局列表 	//link by file->f_list
free_list	//"未使用"file对象列表，可作为file对象的cache, file->f_count = 0;
anon_list	//"在使用"但未分配给超级块的file对象，file->f_count = 1;
sb->s_files	//"在使用"已分配给超级块的file对象



目录项对象
-------------------------------------------------------
路径中的每一部分都对应于一个dentry对象
存在于名为dentry_cache的slab中
struct dentry
{
	struct inode*		d_inode;
	struct dentry*		d_parent;
	struct list_head 	d_hash;		//link in dentry_hash
	struct list_head 	d_lru;		//link in 未使用队列
	struct list_head 	d_child;	//link in 父目录项
	struct list_head 	d_subdirs;	//子目录项列表
	struct list_head 	d_alias;	//link in inode
	struct qstr 		d_name;		//文件名
	unsigned char		d_iname;	//短文件名
}

全局列表		//dentry->d_list
inode->i_dentry		//在使用的，link by dentry->d_alias，一个inode可能有多个dentry
dentry_unused;		//未使用的LRU列表, link by dentry->d_lru
负状态



全局hash表
dentry_hashtable


进程相关结构
--------------------------------------------------------
struct fs_struct			//表示进程与文件系统交互所需信息,task->fs
{
	atomic_t 	count;
	struct dentry*	root;
	struct dentry*	pwd;
	struct dentry*	altroot;
	struct vfsmount*rootmnt;
	struct vfsmount*pwdmnt;
	struct vfsmount*altrootmnt;
}

struct files_struct			//表示进程当前打开的文件,task->files
{
	atomic_t	count;
	struct file**	fd;
	struct file**	fd_array;
}



文件系统类型对象
--------------------------------------------------------
struct file_system_type
{
	super_block* (*)()	read_super;	//读取该文件系统超级块的方法
}

全局
static struct file_system_type *file_systems;
register_filesystem();			//将file_system_type放入全局列表file_systems中，每个文件系统不能有相同文件名


已安装的文件系统对象
------------------------------------------------------
struct vfsmount
{
	struct list_head mnt_hash;
	struct vfsmount *mnt_parent;
	struct dentry *mnt_mountpoint;
	struct dentry *mnt_root;
	struct super_block *mnt_sb;
	struct list_head mnt_mounts;	//子文件系统的列表
	struct list_head mnt_child;	//link in 父文件系统的mnt_mounts;
	struct list_head mnt_list;
}

全局列表

全局hashtable
mount_hashtable;	//vfsmount->mnt_hash解决hash冲突






路径名查找
-------------------------------------------------------------
struct nameidata {
	struct dentry *dentry;
	struct vfsmount *mnt;
	struct qstr last;
	unsigned int flags;
	int last_type;
};

path_init
path_walk
path_release

__user_walk;(char* name, nameidata* nd)		//作为wrap函数，被很多系统调用使用
	-getname;	//从用户空间获得数据
	-path_lookup
		-path_init
			-walk_init_root
		-path_wakk
	-putname;

传到path_init的name是一个文件路径
path_init()根据name是从根目录开始还是从当前目录开始，初始化nd->mnt, nd->dentry,指定搜索的起始位置
	如果从根目录开始，调用walk_init_root
	如果从相对目录开始，nd->mnt = current->fs->pwdmnt; nd->dentry = current->fs->pwd
path_walk()
	-link_path_walk
		-permission	//inode检查MAY_EXEC权限
		-follow_dotdot	//查看上层目录
				//开始搜索目录
		-cached_lookup	
			-d_lookup	//dentry_hashtable
		-real_lookup	
			-d_alloc	//从dentry_cache分配一个目录项，初始化
			-parent->d_inode->i_op->lookup(parent->d_inode, dentry)
					//通过父节点inode读取dentry
					//即ext2_lookup
			

文件系统的安装
-------------------------------------------------------------------------
struct namespace {
	atomic_t		count;
	struct vfsmount *	root;
	struct list_head	list;
	struct rw_semaphore	sem;
};


三个mount函数
sys_mount			//系统调用
	copy_mount_options
	do_mount
		do_remount
		do_loopback	//建立/dev/loop0与普通文件之间的关系，命令losetup
		do_move_mount
		do_add_mount
mount_root			//init进程->prepare_namespace->mount_root
	devfs_make_root
	create_dev("/dev/root",);
	rd_load_disk
	mount_block_root
kern_mount			//安装特殊文件系统
	do_kern_mount

1、安装根文件系统
start_kernel->mnt_init
	init_rootfs
		-register_filesystem("rootfs")
	init_mount_tree
		-do_kernel_mount
			-type = get_fs_type
			-mnt = alloc_vfsmnt
			-sb = 	get_sb_bdev	这里复杂,常规文件系统
				get_sb_single	
				get_sb_nodev	无设备文件系统
				-path_lookup
				-fs_type->read_super
				-path_release

2、安装一般文件系统
sys_mount
	do_mount

卸载文件系统
umount


__setup("root=", root_dev_setup);
	root_dev_setup

