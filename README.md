# Maven Dependencies Analyser Examples

This project demonstrates how you can use [Maven Dependencies Analyser](https://github.com/aistomin/maven-dependencies-analyser)
library. 

If you clone the repository and run ```mvn clean install package```
in the project's folder, the build will fail with the error like:
```
[ERROR] Failed to execute goal com.github.aistomin:maven-dependencies-analyser:0.1.1:check (default) on project maven-dependencies-analyser-examples: com.github.aistomin:maven-browser (version 1.2) has newer versions: 1.4; 1.3 -> [Help 1]
```
It fails because the analyser detects the out-dated library ```maven-browser```.

The configuration responsible for this validation is in the ```pom.xml```:
```
<plugin>
    <groupId>com.github.aistomin</groupId>
    <artifactId>maven-dependencies-analyser</artifactId>
    <version>0.1.1</version>
    <configuration>
        <level>ERROR</level>
    </configuration>
    <executions>
        <execution>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

If you like to make this configuration less extreme and only show the
 warning in case one of the dependencies is out of date, just change
 ```<level>ERROR</level>``` to ```<level>WARNING</level>```. Try ```mvn clean install package```
 again and the build will be successful. In the build output you'll see the warning:
```
[WARNING] com.github.aistomin:maven-browser (version 1.2) has newer versions: 1.4; 1.3
```