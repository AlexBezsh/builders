### Maven build:
- with tests: ```mvn clean package```
- without tests: ```mvn clean package -DskipTests```
- only tests: ```mvn test```

### Gradle build:
- with tests: ```gradle clean build```
- without tests: ```gradle clean build -x test```
- only tests: ```gradle test```