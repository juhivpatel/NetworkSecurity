# NetworkSecurity
Instructions on how to run this poject
Download STS from https://spring.io/tools/sts/all 
Download the project from github.
Download MYSQL server from https://dev.mysql.com/downloads/cluster/
While installing the sql server you will get your default password to sql server. Copy the password in a text file to change it later to your desirable password (choose passwrod root if you don't want to make any changes in the actual code)
Start the aql server.
Go to terminal type command "pwd".
Type command "ls -al" to see a list of file.
Check if you have a file called bash_profile. If not create a file and enter "export PATH=${PATH}:/usr/local/mysql/bin/" in the file. If the file alreay exst get rid of the specified path and enter the above path.
Then enter command "mysql -u root -p". If it says comand not found open another terminal window and type the same command. It will prompt you to enter password. Enter password that you saved in the text file while instaling sql server.
Once uder the sql server type the command "ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';".
Now download MySQL workbench from https://dev.mysql.com/downloads/workbench/ 
Open MySQL wrokbench under the server and create a database instance with following details:
connection name: local Instance, HostName: localhost, port: 3306
Create a new database names "userbase" and run the following script:



CREATE  TABLE users (
  userid VARCHAR(5) NOT NULL,
  username VARCHAR(45) NOT NULL ,
  password VARCHAR(60) NOT NULL ,
  enabled TINYINT NOT NULL DEFAULT 1 ,
  PRIMARY KEY (userid));
   
CREATE TABLE user_roles (
  user_role_id int(11) NOT NULL AUTO_INCREMENT,
  userid varchar(5) NOT NULL,
  role varchar(45) NOT NULL,
  PRIMARY KEY (user_role_id),
  UNIQUE KEY uni_username_role (role,userid),
  KEY fk_username_idx (userid),
  CONSTRAINT fk_username FOREIGN KEY (userid) REFERENCES users (userid));
 
INSERT INTO users(userid,username,password,enabled)
VALUES ('001','admin','$2a$04$pz76kI9suPDuyq7DI9kWYu7cINbJY77M12o288K6KNGzpR6L9PM5e', true);
INSERT INTO users(userid,username,password,enabled)
VALUES ('002','user','$2a$04$sWLYoSU8PZHk8TZFkxlZ5.mEWmz4cS5c6Q9TfluqKq6Z4SBFpY42C', true);
 
INSERT INTO user_roles (userid, role)
VALUES ('002', 'ROLE_USER');
INSERT INTO user_roles (userid, role)
VALUES ('001', 'ROLE_ADMIN');
INSERT INTO user_roles (userid, role)
VALUES ('001', 'ROLE_USER');



Thus our database is now created.
Open STS, import the project and run it using maven build.
Edit configuration by cahnging goals to "clean install spring-boot:run".
STS will start embeded tomcat server.
Now open localhost:8080 and you will get welcome page.
