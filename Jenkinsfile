pipeline {
	environment {
		pm_config = 'yohanlakhani.com'
		ew_id = '4740'
		ew_ver = '1.5'
    	}
	agent {
        	docker {
        	    	image 'akamai/shell'
        	}

    	}
	options {
		skipDefaultCheckout(true)
	}
	stages {
		stage ("Checkout EW"){
			steps {
				checkout scm
			}
		}
		stage ("Package"){
                        steps {
				sh 'echo EWiD: ${ew_id}'
                                sh 'ls -lrt'
				sh 'rm ew-helloworld.tgz'
				sh 'ls -lrt'	
                                sh 'tar -czvf ew-helloworld.tgz *'
                                sh 'ls -lrt'
                        }		
		}
		stage ("Update"){
			steps {
				sh "akamai edgeworkers upload --bundle ew-helloworld.tgz ${ew_id} --section default"
			}
		}
        stage ("Activate: Staging"){
            steps {
                sh "akamai edgeworkers --section default activate ${ew_id} STAGING ${ew_ver}"
            }
        }
        stage ("Test: Staging"){
            steps {
                sh "------------------------------------------------------------------"
				sh "------------------* DONT FORGET! DO YOUR TEST *-------------------"
				sh "------------------------------------------------------------------"
				sh "----------------------------* Yay *-------------------------------"
				sh "------------------------------------------------------------------"
            }
        }
        stage ("Activate: Prod"){
            steps {
                sh "akamai edgeworkers --section default activate ${ew_id} PRODUCTION ${ew_ver}"
            }
        }				
	}
}
