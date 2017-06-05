---
title: Unit Testing Primer in Java
description: Unit testing primer in java using depedency injection, JUnit, and Mockito
header: Unit Testing Primer in Java
tags: [testing]
---
Ensuring your code is working properly can be done in different ways, unit testing being one of them.  People define unit testing in different ways.  In java speak I consider unit testing as testing a method in a class and have this method isolated from dependencies.  There are different frameworks that can help do this including JUnit and Mockito.

In our example we will be testing a common scenario. An object that handles business logic calling another object that is used for persistance. 

### Tools
The following will be used to perform the unit tests
* [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection)
* [JUnit](http://junit.org/junit4/)
* [Mockito](http://site.mockito.org/)
* [Maven](https://maven.apache.org/)

### Classes
These are the classes that we will be using in the unit test example
* ```Pojo.java``` - This is a POJO used as a data container.
{% highlight java %}
package com.rodrod.unittest;

public class Pojo {

  private Integer id;
  private String name;

  public Integer getId() {
    return id;
  }

  public void setId(Integer id) {
    this.id = id;
  }

  public String getName() {
    return name;
  }
  public void setName(String name) {
    this.name = name;
  }
}
{% endhighlight %}
* ```BusinessLogic.java``` - This contains method createPojo that has some logic that we will be testing.  It also has a dependency on the Persitence class.
{% highlight java %}
package com.rodrod.unittest;

import java.util.Optional;

public class BusinessLogic {
  private final Persistence persistence;

  public BusinessLogic(Persistence persistence) {
    this.persistence = persistence;
  }

  public Pojo createPojo(Pojo pojo) {

    if (pojo.getName() == null || pojo.getName().trim() == "") {
      throw new IllegalArgumentException("Name is required");
    }

    Optional<Pojo> existingPojo = persistence.getPojoByName(pojo.getName());

    if (existingPojo.isPresent()) {
      return existingPojo.get();
    } else {
      persistence.doSomething();
    }

    return persistence.createPojo(pojo);
  }
}
{% endhighlight %}

* ```Persitence.java``` - This respresents a class that would be persisting to a data store.  The impelemntation of the methods are not relevent since we will be mocking this class.
{% highlight java %}
package com.rodrod.unittest;

import java.util.Optional;

public class Persistence {

  public Optional<Pojo> getPojoByName(String name) {
    Pojo pojo = new Pojo();
    pojo.setName(name);
    return Optional.of(pojo);
  }

  public Pojo createPojo(Pojo pojo) {
    pojo.setId(0);
    return pojo;
  }

  public boolean doSomething() {
    return true;
  }

}
{% endhighlight %}

* ```BusinessLogicTest.java```  -  This is the class that will be performing the unit tests on the BusinessLogic class.  The focus will be on this class.
{% highlight java %}
package com.rodrod.unittest;

import org.junit.Before;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;
import org.junit.runner.RunWith;
import org.mockito.Mock;
import org.mockito.runners.MockitoJUnitRunner;

import java.util.Optional;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.never;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

@RunWith(MockitoJUnitRunner.class)
public class BusinessLogicTest {

  private BusinessLogic businessLogic;
  private Pojo pojo;
  private String name = "TestName";

  @Mock
  private Persistence mockPersistence;

  @Rule
  public ExpectedException thrown = ExpectedException.none();

  @Before
  public void setup() {
    businessLogic = new BusinessLogic(mockPersistence);
    pojo = new Pojo();
    pojo.setName(name);
  }

  @Test
  public void testCreatePojoWithValidNameShouldReturnWithAnId() {
    int id = 123;
    Pojo createdPojo = new Pojo();
    createdPojo.setId(id);
    createdPojo.setName(pojo.getName());

    when(mockPersistence.getPojoByName(name)).thenReturn(Optional.empty());
    when(mockPersistence.createPojo(pojo)).thenReturn(createdPojo);

    Pojo returnedPojo = businessLogic.createPojo(pojo);

    assertEquals(name, returnedPojo.getName());
    assertEquals(id, returnedPojo.getId().intValue());
    verify(mockPersistence).doSomething();
  }

  @Test
  public void testCreatePojoWithEmptyNameShouldThrowIllegalArgumentException() {
    pojo.setName("");

    thrown.expect(IllegalArgumentException.class);
    thrown.expectMessage("Name is required");

    businessLogic.createPojo(pojo);
  }

  @Test(expected = IllegalArgumentException.class)
  public void testCreatePojoWithEmptyNullShouldThrowIllegalArgumentException() {
    pojo.setName(null);

    businessLogic.createPojo(pojo);
  }

  @Test
  public void testCreatePojoWithExistingNameShouldRetrunTheExisting() {
    Pojo existingPojo = new Pojo();

    when(mockPersistence.getPojoByName(name)).thenReturn(Optional.of(existingPojo));

    Pojo createdPojo = businessLogic.createPojo(pojo);

    assertEquals(existingPojo, createdPojo);
    verify(mockPersistence, never()).doSomething();
  }

}

{% endhighlight %}
### Unit Testing Details
Here is an explanation





