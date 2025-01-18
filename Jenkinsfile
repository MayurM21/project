pipeline {
	
	agent {
		node{
		label "master"
		customWorkspace "/home/mayur/project"

}
}	     
	      stages {

		     stage ("clone") {
				
				steps { 
					sh "sudo rm -rf /home/mayur/project/project/"
					sh "sudo git clone https://github.com/MayurM21/project.git -b dev"
					sh "sudo chmod -R 777 /home/mayur/project"
				

}

}

		    stage ("compile") {
				
				steps {
					sh "sudo rm -rf /home/mayur/.m2/repository"
					sh "mvn -f /home/mayur/project/project/pom.xml clean install"
}
}					

		    stage ("deploy") {
				
				steps {
					sh "sudo scp -i /home/mayur/mayur.pem -o StrictHostKeyChecking=no /home/mayur/project/project/target/LoginWebApp.war mayur@3.110.122.162:/home/mayur/servers/apache-tomcat-9.0.98/webapps"	
					
				
}
}



		    stage ("starting server") {
			agent {
			 node {
			 label "dev"	
		
}

}
				steps {
		            sh "chmod -R 777 /home/mayur/servers/apache-tomcat-9.0.98/webapps/LoginWebApp.war"
					sh "nohup bash /home/mayur/servers/apache-tomcat-9.0.98/bin/shutdown.sh &"
					sh "nohup bash /home/mayur/servers/apache-tomcat-9.0.98/bin/startup.sh &"
}


}

}
}
