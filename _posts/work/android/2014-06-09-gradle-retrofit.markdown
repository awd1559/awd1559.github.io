---
layout:     post
title:      "retrofit"
subtitle:   " \"Android retrofit by square\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[retrofit](https://github.com/square/retrofit)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


# install 
```
compile 'com.squareup.retrofit2:retrofit:2.0.2'
```

# usage

```
public interface GitHubService {
  @GET("users/{user}/repos")
  Call<List<Repo>> listRepos(@Path("user") String user);
}

Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .build();

GitHubService service = retrofit.create(GitHubService.class);

Call<List<Repo>> repos = service.listRepos("octocat");
```

# api

#### Request

```
@GET, @POST, @PUT, @DELETE, @HEAD

@GET("users/list")
@GET("users/list?sort=desc")

```

#### parameters

```
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId);

@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @Query("sort") String sort);

@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @QueryMap Map<String, String> options);
```

#### request body

```
@POST("users/new")
Call<User> createUser(@Body User user);
```

#### form Encoded

```
@FormUrlEncoded
@POST("user/edit")
Call<User> updateUser(@Field("first_name") String first, @Field("last_name") String last);
```

#### Multipart

```
@Multipart
@PUT("user/photo")
Call<User> updateUser(@Part("photo") RequestBody photo, @Part("description") RequestBody description);
```

#### Header

```
@Headers("Cache-Control: max-age=640000")
@GET("widget/list")
Call<List<Widget>> widgetList();


@Headers({
    "Accept: application/vnd.github.v3.full+json",
    "User-Agent: Retrofit-Sample-App"
})
@GET("users/{username}")
Call<User> getUser(@Path("username") String username);


@GET("user")
Call<User> getUser(@Header("Authorization") String authorization)

```


