pipeline{
    agent any

    environment{
        JUNIT_PATH = "C:\\Users\\user\\.m2\\repository\\org\\junit\\platform\\junit-platform-console-standalone\\1.10.2\\junit-platform-console-standalone-1.10.2.jar"
    }

    stages{

        stage('Checkout'){
            steps {
                checkout scm
            }
        }

        stage('Build'){
            steps{
                //
                bat '''

                REM Compile the classes
                javac -encoding UTF-8 -d classes "src\\main\\java\\org\\example\\*.java"

                REM Compile the test classes
                javac -encoding UTF-8 -d classes -cp "%JUNIT_PATH%;classes;" "src\\test\\java\\org\\example\\*.java"

                '''

            }
        }
        stage('Test'){
            steps{
//                 echo 'Testing the project'
                bat '''

                REM Run the tests
                java -cp "%JUNIT_PATH%;classes" org.junit.platform.console.ConsoleLauncher --scan-class-path > test_result.txt

                '''
            }
        }
    }
    post{
        always{
            archiveArtifacts 'test_result.txt'
        }
        failure{
            echo 'Build or test failed'
        }
        success{
            echo 'Build or test succeeded'
        }
    }

}