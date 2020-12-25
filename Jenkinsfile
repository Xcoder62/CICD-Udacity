pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'echo "Hello World"'
        sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
      }
    }

    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }

    stage('Upload to S3') {
      agent any
      steps {
        echo 'Uploading to S3'
        withAWS(credentials: 'cidi-user', region: 'us-west-2')
        s3Upload(bucket: 'shark-s3-bucket', pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', acl: 'PublicRead')
      }
    }

  }
}