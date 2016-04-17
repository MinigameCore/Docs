---
layout: page
title: IDE Setup
---

### Adding Dependencies

To use MinigameCore in your plugin, you must add MinigameCore as a Maven or Gradle dependency. MinigameCore is hosted on the [JitPack](https://jitpack.io/) repository.
		
#### Gradle

1. In your `build.gradle` file, add the JitPack repository.

        repositories {
            maven { url "https://jitpack.io" }
        }
		
1. Add the MinigameCore dependency to your `build.gradle`. Replace `VERSION` with a valid tag on GitHub.

        dependencies {
            compile 'com.github.MinigameCore:MinigameCore:VERSION'
        }
        
1. Install the shadow plugin.

        plugins {
            id 'com.github.johnrengelman.shadow' version '1.2.3'
        }

        artifacts {
            archives shadowJar
        }
        
1. Include MinigameCore in the JAR and relocate it to your package. Replace `YOUR.PLUGIN.PACKAGE` with your plugin package.

        shadowJar {
            dependencies {
                include dependency('com.github.MinigameCore:MinigameCore')
            }

            relocate 'io.github.flibio.minigamecore', 'YOUR.PLUGIN.PACKAGE.minigamecore'
        }
		
1. Refresh your Gradle dependencies.

**You are now ready to develop plugins with MinigameCore!**

-----

#### Maven

1. In your `pom.xml` file, add the JitPack repository inside of the `repositories` tags.

        <repositories>
          <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
          </repository>
        </repositories>
	
1. Add the MinigameCore dependency to your `pom.xml` file inside of the `dependencies` tags. Replace `VERSION` with a valid tag on GitHub.

        <dependencies>
          <dependency>
            <groupId>com.github.MinigameCore</groupId>
            <artifactId>MinigameCore</artifactId>
            <version>VERSION</version>
          </dependency>
        </dependencies>
    
1. Add the shade plugin to your `pom.xml` file, and relocate MinigameCore to your package. Replace `YOUR.PLUGIN.PACKAGE` with your plugin package.

        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.4.3</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <relocations>
                                <relocation>
                                    <pattern>io.github.flibio.minigamecore</pattern>
                                    <shadedPattern>YOUR.PLUGIN.PACKAGE.minigamecore</shadedPattern>
                                </relocation>
                            </relocations>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
		
1. Refresh your Maven dependencies.

**You are now ready to develop plugins with MinigameCore!**
