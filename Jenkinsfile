#!groovy

node {
	//--------------------------------------------------------------------------
	//                       CICLO FOR para las STAGES 
	//--------------------------------------------------------------------------
	for(int i=0; i<3; i++) {
		stage "Stage Num" +i
		print 'Hello World, $i!'
	}
	//--------------------------------------------------------------------------
	//                       ETAPA Checkout
	//--------------------------------------------------------------------------
	stage 'Checkout source master'
	//git url: 'git://github.com/arlenesr28/testing.git',
    //	branch: 'master'

    //checkout scm 

    	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '593d0524-8364-4335-89d3-fc0bed5ed382', url: 'https://github.com/arlenesr28/testing.git']]])
    	echo 'configuracion scm'

	//--------------------------------------------------------------------------
	//                       ETAPA Set Version
	//--------------------------------------------------------------------------
	// Prepare the version by extracting major and minor number and creating a new number: [major].[minor]-[BUILDNUMBER]
    
    //stage 'Set Version'
    //def originalV = version();
    //def major = originalV[0];
    //def minor = originalV[1];
    //def v = "${major}.${minor}-${env.BUILD_NUMBER}"
    //if (v) {
    //   echo "Building version ${v}"
    //}

    	//readFile encoding: 'UTF-8', file: '/testing/Jenkinsfile'

	//--------------------------------------------------------------------------
	//                       ETAPA Test
	//--------------------------------------------------------------------------
	stage 'Test'
	echo 'Ejecutando tests'
	try {
		import unittest2 as unittest
	}
	catch(Exception e) {
		import unittest
	}

	node ('Probando_calculadora') {
		class SimpleTest(unittest.TestCase):
		    @unittest.skip("demonstrating skipping")
		    def test_skipped(self):
			self.fail("shouldn't happen")

		    def test_pass(self):
			self.assertEqual(10, 7 + 3)

		    def test_fail(self):
			self.assertEqual(11, 7 + 3)
	}
	
	//--------------------------------------------------------------------------
	//                       ETAPA Release
	//--------------------------------------------------------------------------
	stage 'Release Build'
	sshagent(['593d0524-8364-4335-89d3-fc0bed5ed382']) //Mis credenciales de github que estan guardadas en Jenkins
    // Push the commit and the created tag
    	bat returnStatus: true, script: '''git add calculadora.py
	git commit -m "Haciendo pruebas......."
	git status
	git pull origin master
	git push -u origin master'''

	echo 'pull & push testing.....'
      //sh "git push origin master"
      //sh "git push origin v${v}"


	//--------------------------------------------------------------------------
	//                       ETAPA
	//--------------------------------------------------------------------------
	//stage 'uipuipoi'
}
