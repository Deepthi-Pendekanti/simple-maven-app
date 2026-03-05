# simple-maven-app
# Create GitHub Repository
Go to **GitHub → New Repository**
# Create Maven Project Structure in GitHub

Create files using **Add file → Create new file**.
Final structure must look like:
program1-maven-demo
│
├── pom.xml
│
└── src
    ├── main
    │   └── java
    │        └── Program1.java
    │
    └── test
        └── java
             └── Program1Test.java
#  Java Program

Create file:
src/main/java/Program1.java
Paste:
java
public class Program1 {

    public static String message() {

        return "This is Program 1 - Maven Jenkins Demo";

    }

    public static void main(String[] args) {

        System.out.println(message());

    }

}
# Test Script (JUnit)

Create file:

```
src/test/java/Program1Test.java
```

Paste:

```java
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;

public class Program1Test {

    @Test
    void testMessage() {

        assertEquals(
            "This is Program 1 - Maven Jenkins Demo",
            Program1.message()
        );

    }

}
This test checks whether the **Program1 message() method returns the correct output**.

# pom.xml

Create file:

```
pom.xml
```

Paste:
<project xmlns="http://maven.apache.org/POM/4.0.0"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
 http://maven.apache.org/xsd/maven-4.0.0.xsd">

 <modelVersion>4.0.0</modelVersion>

 <groupId>com.example</groupId>
 <artifactId>program1</artifactId>
 <version>1.0</version>

 <packaging>jar</packaging>

 <dependencies>

  <dependency>
   <groupId>org.junit.jupiter</groupId>
   <artifactId>junit-jupiter</artifactId>
   <version>5.9.0</version>
   <scope>test</scope>
  </dependency>

 </dependencies>

</project>
# Clone Repository to Local System

Open **CMD**

Run:

```
git clone https://github.com/YOUR_USERNAME/program1-maven-demo.git
Enter project folder:
cd program1-maven-demo
Check files:
dir
You should see:
pom.xml
src
# Test Maven Build Locally

Run:

```
mvn clean test
```

Expected output:
Tests run: 1
BUILD SUCCESS
# Configure Maven in Jenkins

Open Jenkins:

```
http://localhost:8080
```

Go to:

```
Manage Jenkins
→ Global Tool Configuration
```

Under Maven:

```
Name: MAVEN
MAVEN_HOME: C:\Program Files\apache-maven-3.9.12
```

Click **Save**.

---

# Create Jenkins Pipeline Job

Click:

```
New Item
```

Name:

```
PROGRAM1_MAVEN_PIPELINE
```

Select:

```
Pipeline
```

Click **OK**.

---

#  Jenkins Pipeline Script

Paste this:
pipeline {

    agent any

    tools {
        maven 'MAVEN'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/YOUR_USERNAME/program1-maven-demo.git'
            }
        }

        stage('Build & Test') {
            steps {
                bat 'mvn clean test'
            }
        }

    }

}
```

Replace

```
YOUR_USERNAME
```

with your GitHub username.

Click **Save**.
run the build

