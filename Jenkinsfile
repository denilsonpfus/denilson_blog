node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build docker images') {
        /* This builds the actual jekyll image; synonymous to
         * docker build on the command line */
      dir('jekyll') {
        app = docker.build("denilsonpfus/jekyll:${env.BUILD_NUMBER}")
      }
      dir('apache') {
        app = docker.build("denilsonpfus/apache:${env.BUILD_NUMBER}")
      }    
    }
        
    stage('Test docker images') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage ('Launch docker containers') {
      try {
      // Lauch Jekyll container here
           sh "docker run -v /home/denferreira/denilson_blog:/data --name denilson_blog${env.BUILD_NUMBER} denilsonpfus/jekyll:${env.BUILD_NUMBER}" 
      // Lauch Apache container here
           sh "docker run -d -P --volumes-from denilson_blog${env.BUILD_NUMBER} --name apache_server${env.BUILD_NUMBER} denilsonpfus/apache:${env.BUILD_NUMBER}"
      
      } catch (error) {
      } finally {
      // Stop and remove database container here
      //sh 'docker-compose stop db'
      //sh 'docker-compose rm db'
        }
    }

/*    
    stage ('Test application') {
      try {
      // Start Jekyll container here
           sh "docker run -v /home/denferreira/denilson_blog:/data --name denilson_blog${env.BUILD_NUMBER} denilsonpfus/jekyll" 
      // Start Apache container here
           sh "docker run -d -P --volumes-from denilson_blog${env.BUILD_NUMBER} --name apache_server${env.BUILD_NUMBER} denilsonpfus/apache" 
      
      } catch (error) {
      } finally {
      // Stop and remove database container here
      //sh 'docker-compose stop db'
      //sh 'docker-compose rm db'
        }
    }
*/
    
    
    
    
    /*    stage('Push image') {
 *       /* Finally, we'll push the image with two tags:
 *        * First, the incremental build number from Jenkins
 *        * Second, the 'latest' tag.
 *        * Pushing multiple tags is cheap, as all the layers are reused.
 *        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
 *            app.push("${env.BUILD_NUMBER}")
 *            app.push("latest")
 *        }
 *    } */
}
