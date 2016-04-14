---
layout:     post
title:      "greenDAO"
subtitle:   " \"Android greenDAO by greenbot, ORM\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[greenDAO](https://github.com/greenrobot/greenDAO)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


# install

```
compile 'de.greenrobot:greendao:2.1.0'
```


# create dao 

- import new module 'DaoGenerator'
- modify build.gradle(Module: DaoGenerator) 
	srcDir 'src-template'
- add class

```
Schema schema = new Schema(1000, "package.name.dao");

Entity note = schema.addEntity("Note");
note.addIdProperty();
note.addStringProperty("text").notNull();
note.addDateProperty("date");

Entity customer = schema.addEntity("Customer");
customer.addIdProperty();
customer.addStringProperty("name").notNull();

Entity order = schema.addEntity("Order");
order.setTableName("ORDERS");
order.addIdProperty();
Property orderDate = order.addDateProperty("date").getProperty();

Property customerId = order.addLongProperty("customerId").notNull().getProperty();
order.addToOne(customer, customerId);

ToMany customerToOrders = customer.addToMany(order, customerId);
customerToOrders.setName("orders");
customerToOrders.orderAsc(orderDate);

new DaoGenerator().generateAll(schema, "../app/src/main/java");
```

# usage 

```
class DaoExampleApplication extends Application｛
  @Override
  public void onCreate() {
    super.onCreate();
    setupDatabase();
  }

  private void setupDatabase() {
    DaoMaster.DevOpenHelper helper = new DaoMaster.DevOpenHelper(this, "example-db", null);
    SQLiteDatabase db = helper.getWritableDatabase();
    DaoMaster daoMaster = new DaoMaster(db);
    daoSession = daoMaster.newSession();
  }

  public DaoSession getDaoSession() {
    return daoSession;
  }
}

session.getEntityDao()
insertOrReplace(Entity e)
deleteAll()
delete(long id)
load(long id)
List<Entity> loadAll()
```
