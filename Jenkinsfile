def imageName = 'olivier/movies-parser'

node('workers'){
    stage('Checkout'){
        checkout scm
    }

    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Quality Tests'){
        imageTest.inside{
          sh 'golint'
        }
    }

    stage('Unit Tests'){
        imageTest.inside('-u root:root'){
          sh 'go test'
        }
    }

    //stage('Security Tests'){
    //    imageTest.inside('-u root:root'){
    //      sh 'nancy sleuth -p /go/src/github/olivier/movies-parser/Gopkg.lock'
    //    }
    //}
}
