 def imageName = 'mlabouardy/movies-parser'
node('workers') {
    stage('checkout') {
        checkout scm
    }
    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
    stage ('Quality Tests') {
        imageTest.inside{
            sh 'golint'
        }
      stage ('Unit Tests') {
          imageTest.inside{
              sh 'go test'
          }
      }
    }
}           
