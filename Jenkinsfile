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
      steps {
        echo 'Uploading to S3'
        s3Upload(bucket: 'shark-s3-bucket', pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', metadatas: 'fromJenkins', acl: 'PublicRead')
      }
    }

  }
}