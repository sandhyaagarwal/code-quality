# sonar-qube
Using Sonar Qube for maintaining code quality

Sonar Qube is a widely used product for analyzing code for :

* Bugs
* [Code Smells](https://en.wikipedia.org/wiki/Code_smell)
* Vulnerabilities

Follow the steps mentioned below to get started :

* Install the [Sonar Qube server](https://www.sonarqube.org/downloads/) 
* Start the server. The HTTP server listens on port 9000 by default
* Sonar Qube supports multiple DBs. By default, it uses the [H2](http://www.h2database.com/html/main.html) database engine, which is not recommended for using the product at scale
* To change the DB settings, locate **sonar.properties** in the conf folder, relative to the installation folder and update the following properties for the DB (MySQL, Oracle, PostgreSQL, Microsoft SQLServer)

    * sonar.jdbc.url
    * sonar.jdbc.username
    * sonar.jdbc.password
*  Restart the server. All the DB tables are created when SonarQube is started
*  To integrate with maven, locate settings.xml in the conf folder, relative to the maven installation folder
*  Add a new profile as mentioned below :

    <profile>
			<id>sonar</id>
			<activation>
				<activeByDefault>true</activeByDefault>
			</activation>
			<properties>				
			    <!-- SERVER ON LOCAL HOST -->
				<sonar.host.url>http://localhost:9000</sonar.host.url>
			</properties>
	</profile>
    
 *  Add a new pluginGroup for the sonar scanner, as mentioned below
 
        <pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
        
 * Execute the maven lifecycle commands to clean, compile, package and install the project
 * Run mvn sonar:sonar to run static analysis on your maven project
 * Check the results by navigating to the project in the web application
