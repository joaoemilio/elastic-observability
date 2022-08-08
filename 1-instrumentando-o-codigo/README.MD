[setup-your-environment]

[hosts]
# Prevent CORS issues
Add 127.0.0.1 petclinic.com to your hosts file
This is to workaround angular deployment that calls APIs. Once we move it to GCP it is just a matter of updating the alias to point to the Public IP address

[JAVA-AGENT]
> Faça o Download do agent apm para Java mais atual
https://search.maven.org/search?q=g:co.elastic.apm%20AND%20a:elastic-apm-agent

```wget https://repo1.maven.org/maven2/co/elastic/apm/elastic-apm-agent/1.33.0/elastic-apm-agent-1.33.0.jar```

> Siga essa documentação:
https://www.elastic.co/guide/en/apm/agent/java/current/setup-javaagent.html#setup-generic

> Diretamente no Kibana:
. Clique em Integrations
. Elastic APM
. Siga as instruções da Linguagem de programação desejada

> Atualize o script mvnw com as instruções do agent

exec "$JAVACMD" \
  -javaagent:/home/ec2-user/elastic-apm-workshop/petclinic-backend/elastic-apm-agent-1.33.0.jar \
  -Delastic.apm.service_name=petclinic-backend \
  -Delastic.apm.server_urls=https://e93c878a5ff845e0bee2d3096b0d9ab5.apm.us-east-1.aws.cloud.es.io:443 \
  -Delastic.apm.secret_token=OvGtw3H1fEMLDEgW4i \
  -Delastic.apm.environment=production \
  -Delastic.apm.application_packages=org.springframework.samples.petclinic \
  $MAVEN_OPTS \
  -classpath "$MAVEN_PROJECTBASEDIR/.mvn/wrapper/maven-wrapper.jar" \
  "-Dmaven.home=${M2_HOME}" "-Dmaven.multiModuleProjectDirectory=${MAVEN_PROJECTBASEDIR}" \
  ${WRAPPER_LAUNCHER} $MAVEN_CMD_LINE_ARGS

## ANGULAR (RUM)
There are two things to be done:
1 - Install the Angular RUM module
> npm install @elastic/apm-rum-angular --save

2 - Update the code app.module.ts

Follow this documentation:
> https://www.elastic.co/guide/en/apm/agent/rum-js/current/angular-integration.html