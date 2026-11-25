# Anypoint Platform Development: Production-Ready Development Practices - DEX660

## Local Path
- PROJECT_HOME=/Users/yehan.jeong/Desktop/dex660-202611
- STUDENT_FILE=/Users/yehan.jeong/Desktop/DEX660-WI27-EN-Student-Files

## Anypoint Platform Information
- Mule Account: yehan202611

### Business Group
- Business Group ID: 8c632c6e-c721-49a3-926b-9aefb5d3dce3
- Client ID: b406b5f66b144c288145178cdf0c7814
- Client Secret: 3E1240DDEEDB48D59ebeAc4D7CA5E4FC

### Connected App 
- Exchange Contributor ID: 
- Exchange Contributor Secret: 
- CloudHub Deployment ID: 
- CloudHub Deployment Secret: 

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
