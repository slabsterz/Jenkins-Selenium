pipeline {
    agent any

    environment {
        CHROME_VERSION = '127.0.6533.73'
        CHROMEDRIVER_VERSION = '127.0.6533.72'
        CHROME_INSTALL_PATH = 'C:\\Program Files (x86)\\Google\\Chrome\\Application'
        CHROMEDRIVER_PATH = '"C:\\Program Files (x86)\\Google\\Chrome\\Application\\chromedriver.exe"'
    }

    stages {
        stage('Checkout code') {
            steps {
                git branch: 'main', url: 'https://github.com/slabsterz/Jenkins-Selenium\\SeleniumIDE.git'
            }
        }
    }
}