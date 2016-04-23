---
layout:     post
title:      "Dagger"
subtitle:   " \"Android Dagger by square & google\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[dagger1 by square](https://github.com/square/dagger)</small>
><small>[dagger2 by google](https://github.com/square/dagger)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


dependency injector - by [square](https://square.github.io)

use dagger2 by google


# install

```
compile 'com.google.dagger:dagger:2.0'
compile 'com.google.dagger:dagger-compiler:2.0'
compile 'javax.annotation:javax.annotation-api:1.2'
```

# usage 

```
@Inject
@Module
@Provide
@Component
@Scope
```




```
//create model
public class Motor {

    private int rpm;

    public Motor(){
        this.rpm = 0;
    }

    public int getRpm(){
        return rpm;
    }

    public void accelerate(int value){
        rpm = rpm + value;
    }

    public void brake(){
        rpm = 0;
    }
}

public class Vehicle {

    private Motor motor;

    @Inject
    public Vehicle(Motor motor){
        this.motor = motor;
    }

    public void increaseSpeed(int value){
        motor.accelerate(value);
    }

    public void stop(){
        motor.brake();
    }

    public int getSpeed(){
        return motor.getRpm();
    }
}
```


```
//create module 

@Module
public class AppModule {
    private final App application;

    public AppModule(App application) {
        this.application = application;
    }

    @Provides
    @Singleton
    App provideApp() {
        Log.e("module", "provideApp");
        return application;
    }

    @Provides
    @Singleton
    Motor provideMotor() {
        return new Motor();
    }

    @Provides
    @Singleton
    Vehicle provideVehicle() {
        return new Vehicle(new Motor());
    }
}
```

```
//component
@Singleton
@Component(modules = AppModule.class)
public interface AppComponent {
    Vehicle vehicle();

    App app();

    void inject(MainActivity activity);
}
```

```
//dagge into application
class App extends Applicaiton {
  private AppComponent component;
  onCreate() {
    DaggerAppComponent.builder().appModule(new AppModule(this)).build();
  }
  public static AppComponent component(Context context) {
    return ((App) context.getApplicationContext()).component;
  }
}
```

```
//use it
@Inject
App app;

@Inject
Vehicle vehicle;

class MainActiviy extends AppCom {
  onCreate() {
    App.component(this).inject(this);
  }
}
```
