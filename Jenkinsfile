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
        withAWS(region: 'us-west-2', credentials: '1e975091-a0fd-4a65-9146-6fff391b465d') {
          s3Upload(bucket: 'shark-s3-bucket', pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', acl: 'PublicRead')
        }

      }
    }

  }
}