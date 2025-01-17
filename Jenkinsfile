pipeline {
	
	agent {
		node{
		label "built-in"
		customWorkspace "/home/ec2-user"

}
}	     
	      stages {

		     stage ("clone") {
				
				steps { 
					sh "sudo rm -rf project"		
					sh "sudo git clone https://github.com/MayurM21/project.git -b dev"
				

}

}

		    stage ("compile") {
				
				steps {
					sh "sudo rm -rf /root/.m2/repository"
					sh "mvn -f /home/ec2-user/project/pom.xml"
					
				
}

}

		    stage ("deploy") {
			agent {
			 node {
			 label "dev"	
		
}

}
				steps {

					sh "sudo scp -i /home/ec2-user/test.pem -o StrictHostKeyChecking=no /home/ec2-user/project/target/LoginWebApp.war ec2-user@172.31.13.159:/home/ec2-user/server/apache-tomcat-9.0.98/webapps"
					sh "nohup .//home/ec2-user/server/apache-tomcat-9.0.98/shutdown.sh &"
					sh "nohup .//home/ec2-user/server/apache-tomcat-9.0.98/startup.sh &"
}


}

}





}
