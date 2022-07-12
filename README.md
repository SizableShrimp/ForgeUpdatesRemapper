# Forge Updates Remapper
**Forge Updates Remapper** is a tool which helps you remap your Forge mod using provided URLs pointing to SRG files.
This tool can also be used in reverse.
This tool only works with **Java source files**.
Other JVM languages are not supported, and support is not planned.

## Note: You MUST run this BEFORE updating/changing anything
For this script to work, your mod must compile as-is.
This means changing your Forge version or Minecraft version first will cause this script to fail.

## How to use this
This guide assumes you are on ForgeGradle 5 or newer.

### 1. Make a backup!
This script changes your mod's sourcecode.
You should make a backup in case anything goes wrong.
If not already, using Git or another version control system is highly recommended, even if private.
You have been warned.

### 2. Add this line to your `build.gradle`
This script can be used by adding the following line to your `build.gradle`:
```groovy
apply from: 'https://raw.githubusercontent.com/SizableShrimp/ForgeUpdatesRemapper/main/remapper.gradle'
```
This should be near the top of the file below ALL other plugins. Here is an example:
```groovy
plugins {
    id 'blah' version '1.0' // Plugins here
}
apply plugin: 'blah' // Other plugins here
// Insert here
apply from: 'https://raw.githubusercontent.com/SizableShrimp/ForgeUpdatesRemapper/main/remapper.gradle'
```

### 3. Run this command
After adding the above line, you are now ready to update your mod by running the provided Gradle task.
You must provide the list of URLs to the SRG files using the `UPDATE_SRGS` property.
If you have more than one URL, separate using a semicolon (`;`).
```shell
gradlew -PUPDATE_SRGS=<insert urls> updateEverything
```

Example:
```shell
gradlew -PUPDATE_SRGS=https://example.com/my_cool_srg.tsrg updateEverything
```

By default, this will only apply to the `main` sourceset. 
If you have an `api` sourceset or other sourcesets, you can add these as well using the `UPDATE_SOURCESETS` property.
This is a semicolon-separated list that can be defined, for example, as `-PUPDATE_SOURCESETS="main;api"`, and would be inserted into the above command before `updateEverything`.

To use this tool in reverse, add `-PREVERSED=true` before `updateEverything`. This will use the provided SRG URLs in the opposite direction, generally for backporting.

### 4. Proceed to update your mod
You can now delete the `apply from:` line from your `build.gradle` and continue updating/backporting your mod.
You should now update your Forge version, mappings, Minecraft version, and anything else as you need to.
You can find the latest Forge version for a given Minecraft release [here](https://files.minecraftforge.net/net/minecraftforge/forge/).
Happy modding!

*If you have any issues, try asking in [the Forge discord](https://discord.minecraftforge.net).*