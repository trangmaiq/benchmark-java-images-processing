# Benchmark Java images-processing

## Getting Started WWith JMK
The easiest way to get started with JMH is to generate a new JMH project using the JHM Maven archetype. The JHM Maven archetype will generate a new Java project with a single, example benchmark Java class, and a Maven `pom.xml` file which contains the correct dependencies to compile and build your JMH micro-benchmarks suite.

Here is the Maven command line needed to generate a JMH project template of my repository.

```
mvn archetype:generate \
-DinteractiveMode=false \
-DarchetypeGroupId=org.openjdk.jmh \
-DarchetypeArtifactId=jmh-java-benchmark-archetype \
-DgroupId=com.github.trangmaiq \
-DartifactId=benchmark-java-images-processing \
-Dversion=0.1
```

This command line will create a new directory named `benchmark-java-images-processing`. Inside the `java` source root directory will be generated a single Java packaged named `com.github.trangmaiq`. And inside `com.github.trangmaiq` package will be a JMH benchmark Java class named `MyBenchmark`.

If everything is okay, here is what you will see:

```java
package com.github.trangmaiq;

import org.openjdk.jmh.annotations.Benchmark;

public class MyBenchmark {

    @Benchmark
    public void testMethod() {
        // This is a demo/sample template for building your JMH benchmarks. Edit as needed.
        // Put your benchmark code here.
    }

}
```

## So... What is next step?
I have a task: Using a jar file that provided before and benchmark it. So to add a dependencies (local file) to my project, 

We can add the dependency to our Maven project by adding those line to our `pom.xml` file:
```xml
<dependency>
            <groupId>com.idrsolutions.image</groupId>
            <artifactId>jdeli</artifactId>
            <version>8.13.23</version>
</dependency>
```

Then we have to execute this command line:
```
mvn install:install-file  -Dfile=jdeli-trial.jar  -DgroupId=com.idrsolutions.image -DartifactId=jdeli -Dversion=8.13.23 -Dpackaging=jar -DgeneratePom=true
```

## Building JMH Benchmark
We can now compile and build a benchmark JAR file from JMH benchmark project using this Maven command:
```
mvn clean install
```
This Maven command must be executed from inside the generated benchmark project directory.

## Running JMH Benchmarks
Once we have built JMH benchmark code, we can run the benchmark using this Java command:
```
java -jar target/benchmarks.jar
```

Running the benchmarks will take some time.

JMH Benchmark Modes
JMH can run your benchmarks in different modes. The benchmark mode tells JMH what you want to measure. JMH offer these benchmark modes:
```
Throughput	        Measures the number of operations per second, meaning the number of times per second your benchmark method could be executed.
Average Time	        Measures the average time it takes for the benchmark method to execute (a single execution).
Sample Time	        Measures how long time it takes for the benchmark method to execute, including max, min time etc.
Single Shot Time	Measures how long time a single benchmark method execution takes to run. This is good to test how it performs under a cold start (no JVM warm up).
All	                Measures all of the above.
```
The default benchmark mode is `Throughput`.
