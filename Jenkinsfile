pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/wlals2/company-infra-finish-c.git'
    }
    stages {
        stage('Checkout') {
            steps {
                // Github 저장소에서 최신 소스 체크아웃
                git branch: 'main', url: "${env.REPO_URL}"
            }
        }
        // 필요하면 아래에 빌드/테스트 단계 추가 가능
        // stage('Build') { ... }
        // stage('Test') { ... }
        stage('Push to GitHub') {
            steps {
                // 예시: 파일 수정 후 자동 푸시까지 할 수 있음
                // sh 'git config --global user.email "you@example.com"'
                // sh 'git config --global user.name "Your Name"'
                // sh 'git add .'
                // sh 'git commit -m "Auto commit from Jenkins" || echo "No changes"'
                // sh 'git push origin main'
                echo "Push는 CLI에서 수동으로, Jenkins는 빌드만 담당 (실습 기준)"
            }
        }
    }
    post {
        always {
            echo 'Jenkins 파이프라인 완료'
        }
    }
}

