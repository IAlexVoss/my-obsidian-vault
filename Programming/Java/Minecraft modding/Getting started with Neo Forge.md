
# First step:

For creating Minecraft mods, the first thing that you need, it's a JDK:

This one, you can make downloaded by the next link: https://adoptium.net/temurin/releases/?package=jdk&version=21&os=any&arch=any

This is a JDK (Java Development Kit) 21 version for windows, or any different OS that you use.

And, during the installation, set up JAVA_HOME variable to local on your hard drive (in the installer)
# Second step

At the second step, you will need the NeoForge MDK, to start creating Minecraft mods:

You may download this by the way: https://github.com/neoforgemdks

You want to clone next repository: https://github.com/NeoForgeMDKs/MDK-1.21-ModDevGradle
After cloning, you want to creating your own repository in your github, for cloning it in the next steps.

# Third step

After previously steps, open IntelliJ Idea, and create the new project with "Clone repository" option

Copying the your HTTPS link to cloning your repository, and just past them into your IntelliJ Idea and just press "Clone" button.

After cloning your repository, check the "Build" button (hammer icon) in the toolbar that located at the top-right corner of the bottom panel
Waiting for successful build before continue.

## After the project initialization

After project initialize, open the "file" option in menu burger on the left up corner of your app window, and click on it. Choose "Project structure" option and choose SDK -> JDK 21 that we already downloaded.

After it, check the your Gradle JVM by the way: Settings -> Build, Execution, Deployment -> Build Tools -> Gradle. In this way, the option Gradle JVM must be accepting the JAVA_HOME: Eclipse Temurin 21.0.X value (Your JDK)

# Customize and rename the example class (Example mod):

Before starting mod development, you need to rename and customize the example mod class.

Find the first line on your ExampleMod file (this is a basic Java class) and find a first row with package. You will need to rename this package to your own alias (that you will thinking).
Select "examplemod" string and press shift + F6 for rename this package in all files in your project. 

Use this template:

> net. + your_alias. + name_of_the_mod

example:

> net.alexvoss.mybestmod

After this, select the name of class "ExampleMod" and renaming it with shift + f6 keyboard combination to your alias.

example:

```Java
@Mod(TutorialMod.MODID)  
public class TutorialMod {
...
}
```



