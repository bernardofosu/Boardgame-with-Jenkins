# BoardgameListingWebApp

## Description

**Board Game Database Full-Stack Web Application.**
This web application displays lists of board games and their reviews. While anyone can view the board game lists and reviews, they are required to log in to add/ edit the board games and their reviews. The 'users' have the authority to add board games to the list and add reviews, and the 'managers' have the authority to edit/ delete the reviews on top of the authorities of users.  

## Technologies

- Java
- Spring Boot
- Amazon Web Services(AWS) EC2
- Thymeleaf
- Thymeleaf Fragments
- HTML5
- CSS
- JavaScript
- Spring MVC
- JDBC
- H2 Database Engine (In-memory)
- JUnit test framework
- Spring Security
- Twitter Bootstrap
- Maven

## Features

- Full-Stack Application
- UI components created with Thymeleaf and styled with Twitter Bootstrap
- Authentication and authorization using Spring Security
  - Authentication by allowing the users to authenticate with a username and password
  - Authorization by granting different permissions based on the roles (non-members, users, and managers)
- Different roles (non-members, users, and managers) with varying levels of permissions
  - Non-members only can see the boardgame lists and reviews
  - Users can add board games and write reviews
  - Managers can edit and delete the reviews
- Deployed the application on AWS EC2
- JUnit test framework for unit testing
- Spring MVC best practices to segregate views, controllers, and database packages
- JDBC for database connectivity and interaction
- CRUD (Create, Read, Update, Delete) operations for managing data in the database
- Schema.sql file to customize the schema and input initial data
- Thymeleaf Fragments to reduce redundancy of repeating HTML elements (head, footer, navigation)

## How to Run

1. Clone the repository
2. Open the project in your IDE of choice
3. Run the application
4. To use initial user data, use the following credentials.
  - username: bugs    |     password: bunny (user role)
  - username: daffy   |     password: duck  (manager role)
5. You can also sign-up as a new user and customize your role to play with the application! 😊

```j

pipeline {
  agent any

  tools {
    maven 'Maven-3.9.11'      // Jenkins > Global Tool Config names
    jdk   'jdk17'
  }

  environment {
    MAVEN_OPTS = '-Dmaven.test.failure.ignore=false'
  }

  stages {

    stage('Git Checkout') {
      steps {
         git branch: 'main', url: 'https://github.com/bernardofosu/Boardgame-with-Jenkins.git'
        // If the repo is private, add: credentialsId: 'github-creds-id'
      }
    }

    stage('Test') {
      when {
        // run tests only when this file changed in the SCM change set
        changeset pattern: 'test.txt', comparator: 'GLOB'
      }
      steps {
        sh 'mvn -B -ntp test'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B -ntp -DskipTests package'
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }

  post {
    always {
      junit 'target/surefire-reports/*.xml'
      cleanWs()
    }
    success {
      echo '✅ Build succeeded'
    }
    failure {
      echo '❌ Build failed – check logs and test reports'
    }
  }
}

```