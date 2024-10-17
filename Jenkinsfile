pipeline {
    agent any
    stages{
        stage('pull') {
            steps {
                script { 
                    build_user = 'jenkins'
                    wrap([$class: 'BuildUser']) {
                        build_user = env.BUILD_USER_ID
                        print("=== BUILD USER: ${build_user}")
                    }
                    print("PROJECT: ${params.PROJECT}")
                    print("SERVICE: ${params.SERVICE}")
                    print("ENV: ${params.ENV}")
                    print("BRANCH: ${params.BRANCH}")
                    print("USER: ${build_user}")
                    /*checkout scm: [
                        $class: 'GitSCM',
                        branches: [[name: env.BRANCH]],
                        userRemoteConfigs: [
                            [url: 'git@bitbucket.org:heliogames/ws-backend.git',
                            refspec: "+refs/heads/${BRANCH}:refs/remotes/origin/${BRANCH}"]
                        ]
                    ]*/
                }
            }
        }
        stage('trigger build') {
            steps {
                build job: "update_service_docker_v2", parameters:
                		[
                			[$class: 'StringParameterValue', name: 'PROJECT', value: PROJECT],                		    
                			[$class: 'StringParameterValue', name: 'SERVICE', value: SERVICE],
                			[$class: 'StringParameterValue', name: 'ENV', value: ENV],                			
                			[$class: 'StringParameterValue', name: 'BRANCH', value: BRANCH]
                		], wait: true	  
            }
        }
    }        
}
