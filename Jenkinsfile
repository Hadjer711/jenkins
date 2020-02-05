
Skip to content
Pull requests
Issues
Marketplace
Explore
@mohmohmoh1999
Learn Git and GitHub without any code!

Using the Hello World guide, you’ll start a branch, write comments, and open a pull request.
mohmohmoh1999 /
TP8

1
0

    0

Code
Issues 0
Pull requests 1
Actions
Projects 0
Wiki
Security
Insights
Settings
TP8/Jenkinsfile
@mohmohmoh1999 mohmohmoh1999 Update Jenkinsfile de6cc26 16 hours ago
59 lines (51 sloc) 1.3 KB
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/**/*.jar'
        archiveArtifacts 'build/docs/**'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'ffffff', body: 'kjsd sdjkbds', to: 'gm_menacer@esi.dz', from: 'gm_menacer@esi.dz', replyTo: 'gm_menacer@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube '
            }

          }
        }

        stage('Test reporting') {
          steps {
            jacoco(execPattern: 'build/jacoco/*.exec', exclusionPattern: '**/test/*.class')
          }
        }

      }
    }

    stage('Deployment') {
when{
branch 'master'
}
      steps {
        bat 'gradle uploadArchives'
      }
    }

    stage('Slack Notification') {
when{
branch 'master'
}
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', channel: '#p', color: '#ff0000', failOnError: true, sendAsText: true, teamDomain: 'p-osu4562', token: 'TT5RR5FMY/BT75V05AP/O6kXurR78Brz0grxGCktV3Wb', username: 'gm_menacer', message: 'build succ')
      }
    }

  }
}

    © 2020 GitHub, Inc.
    Terms
    Privacy
    Security
    Status
    Help

    Contact GitHub
    Pricing
    API
    Training
    Blog
    About

