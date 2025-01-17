pipeline {
	
	agent {
		node{
		label "built-in"
		customWorkspace "/home/mayur"

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
					sh "sudo rm -rf /home/mayur/.m2/repository"
					sh "mvn -f /home/mayur/project/pom.xml"
}
}					

		    stage ("deploy") {
				
				steps {
					sh "sudo scp -i /home/mayur/test.pem -o StrictHostKeyChecking=no /home/mayur/project/target/LoginWebApp.war ec2-user@172.31.13.159:/home/mayur/server/apache-tomcat-9.0.98/webapps"	
					
				
}
}



		    stage ("starting server") {
			agent {
			 node {
			 label "dev"	
		
}

}
				steps {
		
					sh "nohup ./home/mayur/servers/apache-tomcat-9.0.98/shutdown.sh &"
					sh "nohup ./home/mayur/servers/apache-tomcat-9.0.98/startup.sh &"
}


}

}
}


