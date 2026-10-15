pipeline {
    agent any
    environment {
        PYTHON_PATH = 'C:/Users/21210/AppData/Local/Programs/Python/Python312/python.exe'
    }
    stages {
        stage('拉取代码') {
            steps {
                git url: 'https://github.com/peach-Li-y/myflaskapp.git', branch: 'main'
            }
        }
        stage('代码规范检查 flake8') {
            steps {
                bat "${env.PYTHON_PATH} -m pip install flake8"
                bat "${env.PYTHON_PATH} -m flake8 app.py tests/test_app.py"
            }
        }
        stage('安装依赖') {
            steps {
                bat "${env.PYTHON_PATH} -m pip install -r requirements.txt"
            }
        }
        stage('单元测试+覆盖率') {
            steps {
                bat "${env.PYTHON_PATH} -m pytest tests/test_app.py --cov=app --cov-report=html"
            }
        }
    }
    post {
        always {
            echo "流水线执行结束"
        }
    }
}
