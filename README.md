JENKINS PIPELINE DEMO
----------------------------------------------------------------------------

Creating a Jenkins pipeline to retrieve a Spring Boot project from Github
and build it with Maven.

----------------------------------------------------------------------------

**Pipeline script**

```

pipeline {
    agent any

    stages {
        stage ('Printing environment variables') {
            steps {
                echo "Printing environment variables"
                sh '''
                    echo "PATH = ${PATH}"
                    java -version
                    mvn -version
                    git --version
                    docker --version
                ''' 
            }
            
        }

        stage("Cloning Java App from Github") {
            steps {
                echo "Cloning Java App from Github..."
                git 'https://github.com/edgar-code-repository/running-rest-demo-with-docker'
            }
        }

        stage("Building Java App with Maven") {
            steps {
                echo "Building Java App with Maven..."
                sh '''
                    mvn clean package -DskipTests
                 '''
            }
        }

    }

}


```

----------------------------------------------------------------------------