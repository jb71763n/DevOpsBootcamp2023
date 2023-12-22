# Applications

Types of programming languages for this course
- Python
- JavaScript - NodeJS
- Java

Compiled vs Interpereted

Compiled: Only works on the platform it was compiled in.
- Develped
- Compiled
- Executed

Interpereted: implicitly compiled into a byte code and then run
- Developed
- Executed

Interpereted languages convert human readable code to Intermediary Byte Code. The Byte code is then sent to the virtual machine for that language where it is converted to machine code. This means the Interpereted language code can be run on any device that can run the VM for that language.

Example:

- Code is written in python
- it is compiled at run time to byte code and sent to the python virtual machine (VM) where it is converted to machine code. 

All this happens when you run 'python appname.py'

## Packages/Modules/Libraries

Common types
- Filesystems
- Math
- Operating System
- HTTP
- Security
- Networking

Applications use these packages as dependencies

## Build

1. Compile
2. Run tests
3. Package
4. Delivery

- Check build procedure for different types of applications
    + Python
    + Java
    + NodeJS


## Java Introduction

Reasons it is used:
- Free 
- Open-Source
- Huge Community

JDK - Java Development kit

- Develop
    - jdb
    - javadoc
- Build
    - javac
    - jar
- Run
    - JRE (Java Runtime Environment)
    - Java (Command Line Interface)

Prior to version 9, JRE and JDK were separate, after Java 9 both are installed at the same time

## Java Build and Packaging

- Develop source code
    + MyClass.java 
    ```java
    public class MyClass {
        public static void main(String[]args) {
            System.out.println("Hello World");
        }
    }
    ```
- Compile to create executable 
    ```java
    > javac MyClass.java
    MyClass.class
    ```
- Run executable by specifying class name. Note the extention isn't needed
    ```java
    > java MyClass
    Hello World
    ```

Objective is to convert human readable code to byte code to be executed in a Java Virtual Machine (JVM)

Java can be run in any environemnt where a JVM can be run. 

JAR (Java Archive) - Package archiver to compress and combine multiple java files into a single, distributable file. 

WAR (Web Archive) - A web application may also contain static and image files that may be part of the application. 

The JAR or WAR manifest file can be found at META-INF/MANIFEST.MF

The application entry point is specified when the package is created and is listed in the manifest file. Once an application is archived, the archive type is specified when you run it.

```java
> java -jar MyClass
```
To document a java archive, use the javadoc utility
```java
> javadoc -d doc MyClass.java
```
Generates a an HTML document about that source code that other developers can easily browse though and read. 

General Build Process
- Develop
- Compile
- Package
- Document

Build tools to help automate the build processes:
- Maven
- Gradle
- ANT

ANT Uses a Build.xml build file that has sections for Compile, Documentation and Creating executable archive files. 

You can then run the build using the build.xml configuration file rather than performing each step separately. 

Maven and Gradle work in a similar manner. 
