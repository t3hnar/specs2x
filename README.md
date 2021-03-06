# Specs2x [![Build Status](https://secure.travis-ci.org/t3hnar/specs2x.png)](http://travis-ci.org/t3hnar/specs2x)

Extension for [Specs2](http://etorreborre.github.com/specs2/)

## Examples

### DatabaseSpec

Need to create `Database` instance, which will be used in specs

```scala
import specs2x.Database

val database = new Database {
  def start() {
    // setup database
  }

  def withSession[T](f: => T) = {
    // create session
    f
    // submit session
  }

  def stop() {
    // clean and stop database
  }
}
```

Then pass database instance to the specification

```scala
import specs2x.DatabaseSpec

class ExampleDatabaseSpec extends DatabaseSpec(database) {
  "ExampleDatabase" should {
    "insert record" in success  // each will be called in separate session
    "read record"   in success  // also DatabaseSpec is sequential by default
    "delete record" in success  // if any will fail, we will not go further (sequential ^ stopOnFail)
  }
}
```

## Setup

1. Add this repository to your pom.xml:
```xml
    <repository>
        <id>thenewmotion</id>
        <name>The New Motion Repository</name>
        <url>http://nexus.thenewmotion.com/content/repositories/releases-public</url>
    </repository>
```

2. Add dependency to your pom.xml:
```xml
    <dependency>
        <groupId>ua.t3hnar.specs2x</groupId>
        <artifactId>specs2x_2.9.2</artifactId>
        <version>1.0</version>
    </dependency>
```