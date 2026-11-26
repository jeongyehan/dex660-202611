# Anypoint Platform Development: Production-Ready Development Practices - DEX660

## Local Path
- PROJECT_HOME=/Users/yehan.jeong/Desktop/dex660-202611
- STUDENT_FILE=/Users/yehan.jeong/Desktop/DEX660-WI27-EN-Student-Files

## Anypoint Platform Information
- Mule Account: yehan202611 / Password202611

### Business Group
- Business Group ID: 8c632c6e-c721-49a3-926b-9aefb5d3dce3
- Client ID: b406b5f66b144c288145178cdf0c7814
- Client Secret: 3E1240DDEEDB48D59ebeAc4D7CA5E4FC

### Connected App 
- Exchange Contributor ID: 18ae4377357f4039b2530c7a99dd3b71
- Exchange Contributor Secret: 56288Ff78f2C4d0c95c4F505abC016C2
- CloudHub Deployment ID: 598e25a21bae4f9b90d913dca4b131d6
- CloudHub Deployment Secret: 4A993ba8Ab2f41a1A0d5072B292B24e4

### API Instance ID:
- prod: 21319336
- test: 21319361
- dev: 21319353

## Commands
- export PROJECT_HOME=/Users/yehan.jeong/Desktop/dex660-202611
- export STUDENT_FILE=/Users/yehan.jeong/Desktop/DEX660-WI27-EN-Student-Files
- echo $PROJECT_HOME
- echo $STUDENT_FILE
- cd $PROJECT_HOME/check-in-papi/src/main/resources
- PASS="mule12345"
    APP="check-in-papi"
    HOSTNAME="localhost"
    ALTNAMES="DNS:$HOSTNAME,IP:127.0.0.1"
    KEYSTORE="$APP.p12"
    DNAME="cn=$HOSTNAME, ou=Training, o=MuleSoft, c=US"
- keytool -v -genkeypair -keyalg RSA -dname "$DNAME" \
    -ext SAN="$ALTNAMES" -validity 365 -alias server \
    -keystore "$KEYSTORE" -storetype pkcs12 -storepass "$PASS"

- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"lastName\":\"Smith\",\"numBags\":2}" https://localhost:8081/api/v1/tickets/PNR123/checkin

- -M-Danypoint.platform.client_id=b406b5f66b144c288145178cdf0c7814 -M-Danypoint.platform.client_secret=3E1240DDEEDB48D59ebeAc4D7CA5E4FC
- cd $PROJECT_HOME 
- mkdir parent-pom
- cp $STUDENT_FILE/solutions/walkthroughs/devprd/lesson02/wt2-2_solution/parent-pom/pom.xml parent-pom/pom.xml
- mkdir bom
- cp $STUDENT_FILE/solutions/walkthroughs/devprd/lesson02/wt2-2_solution/bom/pom.xml bom/pom.xml
- cp $STUDENT_FILE/solutions/etc/settings.xml.template ~/.m2/settings.xml
- cd $PROJECT_HOME/check-in-papi
- mvn clean verify
- cd $PROJECT_HOME/check-in-papi
- mvn clean deploy
- mvn clean deploy -DmuleDeploy -Dap.client_id=b406b5f66b144c288145178cdf0c7814 -Dap.client_secret=3E1240DDEEDB48D59ebeAc4D7CA5E4FC -Dap.ca.client_id=598e25a21bae4f9b90d913dca4b131d6 -Dap.ca.client_secret=4A993ba8Ab2f41a1A0d5072B292B24e4
- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"lastName\":\"Smith\",\"numBags\":2}" https://check-in-papi-kzvhtj.5sc6y6-2.usa-e2.cloudhub.io/api/v1/tickets/PNR123/checkin
- -M-Denv=test
    -M-Denv=prod
- cd $PROJECT_HOME/check-in-papi
- mvn clean deploy -Dencrypt.key=secure12345
- mvn clean deploy -DmuleDeploy -Dap.client_id=b406b5f66b144c288145178cdf0c7814 -Dap.client_secret=3E1240DDEEDB48D59ebeAc4D7CA5E4FC -Dap.ca.client_id=598e25a21bae4f9b90d913dca4b131d6 -Dap.ca.client_secret=4A993ba8Ab2f41a1A0d5072B292B24e4 -Dencrypt.key=secure12345 -Ddeployment.env=dev
- mvn clean deploy -DmuleDeploy -Dap.client_id=b406b5f66b144c288145178cdf0c7814 -Dap.client_secret=3E1240DDEEDB48D59ebeAc4D7CA5E4FC -Dap.ca.client_id=598e25a21bae4f9b90d913dca4b131d6 -Dap.ca.client_secret=4A993ba8Ab2f41a1A0d5072B292B24e4 -Dencrypt.key=secure12345 -Ddeployment.env=test
- mvn clean deploy -DmuleDeploy -Dap.client_id=b406b5f66b144c288145178cdf0c7814 -Dap.client_secret=3E1240DDEEDB48D59ebeAc4D7CA5E4FC -Dap.ca.client_id=598e25a21bae4f9b90d913dca4b131d6 -Dap.ca.client_secret=4A993ba8Ab2f41a1A0d5072B292B24e4 -Dencrypt.key=secure12345 -Ddeployment.env=prod -Ddeployment.suffix=

- curl -ik -X PUT -H "Content-Type: application/json" -d "{\"lastName\":\"Smith\",\"numBags\":2}" https://localhost:8081/api/v1/tickets/PNR123/checkin
- curl -ik https://localhost:8081/alive
- curl -ik https://localhost:8081/ready
- cd $PROJECT_HOME
- cp check-in-papi/src/main/mule/health.xml apps-commons/src/main/mule/health-common.xml
- cp check-in-papi/src/main/mule/error.xml apps-commons/src/main/mule/error-common.xml
- cd $PROJECT_HOME/apps-commons
- mvn clean install
- cd $PROJECT_HOME
- mvn install:install-file -Dfile=bom/pom.xml -DpomFile=bom/pom.xml
- mvn install:install-file -Dfile=parent-pom/pom.xml -DpomFile=parent-pom/pom.xml
