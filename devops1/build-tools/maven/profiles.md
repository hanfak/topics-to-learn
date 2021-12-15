- Using a profile to run a build.
- Can run each profile using mvn clean verify -P<name of profile>
- Can activate multiple profiles mvn clean verify -P <name of profile>, <name of profile>
- USe of maven-help-plugin, to display active profile at compile time
  - ```
  	<build>
          <plugins>
              <!-- display active profile in compile phase -->
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-help-plugin</artifactId>
                  <version>3.1.0</version>
                  <executions>
                      <execution>
                          <id>show-profiles</id>
                          <phase>compile</phase>
                          <goals>
                              <goal>active-profiles</goal>
                          </goals>
                      </execution>
                  </executions>
              </plugin>

          </plugins>
      </build>
      ```
  - use profiles to set properties
    - ```
    <profile>
      <id>no-tests</id>
      <properties>
          <maven.test.skip>true</maven.test.skip>
      </properties>
    </profile>
    ```
- we can configure many elements such as dependencies, plugins, resources, finalName.
- Activating profile by default
  - ```
  <profile>
    <id>integration-tests</id>
    <activation>
        <activeByDefault>true</activeByDefault>
    </activation>
  </profile>
  ```
  - Dont need to use -P to run the profile
  - If we use the -P, this will use the profile instead of the default one
- Activate automatically, based on env variable -D
  - ```
    <profile>
      <id>active-on-property-environment</id>
      <activation>
          <property>
              <name>environment</name>
          </property>
      </activation>
    </profile>
    ```
  - mvn package -Denvironment
  - Or by the absence
    - ```
      <profile>
          <id>not-active-on-property-environment</id>
          <activation>
              <property>
                  <name>!environment</name>
              </property>
          </activation>
      </profile>
      ```
    - So calling mvn package -Denvironment will not run this profile
