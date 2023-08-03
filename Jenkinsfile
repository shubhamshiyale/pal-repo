pipeline {
       agent any 
	   stages{
	       stage ('move-index') {
		     steps {
			 sh 'echo "this is index.html" > index.html'
			  sh 'aws s3 cp index.html s3://pallavi-7'
			 } 
		   }
         stage ('on-slaves'){
		  parallel {
		     stage ('on-slave1'){
			     agent {
				    label 'QA'
				 }
			    steps {
				   sh 'aws s3 cp s3://pallavi-7/index.html .'
				   sh 'cp -r index.html > /var/www/html/'
				}
			 }
		  stage ('on-slave2'){
		       agent{
			       label 'DEV'
			   }
			  steps {
			    sh 'aws s3 cp s3://pallavi-7/index.html .'
                sh 'cp -r index.html > /var/www/html/'				
			  }
		  }
		  }
		 }
        stage ('restart-httpd'){
		steps {
		sh 'service httpd restart'
		}		 
	   }
      }

}
