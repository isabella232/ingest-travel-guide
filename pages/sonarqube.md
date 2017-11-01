### Sonar
Install the sonar scannae locally (Mac):

```
brew install sonar-scanner
```

Example config file:
```properties
sonar.projectKey=ingest-broker
sonar.projectName=Ingest Broker
sonar.projectVersion=1.0
sonar.sources=.
```

Run sonar scanner

```
sonar-scanner
```