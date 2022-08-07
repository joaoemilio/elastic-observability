[Setup-your-environment]
# Install JDK 11
# Install Nodejs v16, npm 8.5.1, Angular Cli 13.2.4

[petclinic-backend]
run:
'''
mvnw spring-boot:run
'''

[petclinic-frontend]
npm install
ng server

[test]
http://locahost:4200/
