# Build using Gradle

## Compile and Run
There are two types of **Build.gradle** file. In this time we often use which is located in app folder.

#### Build Variant Variables

If you want to change variables depend on build type. Declare **buildTypes**

```
android {
    buildTypes {
        debug{    // Build Variante Type
            buildConfigField("String" /* Variable Type */, "MYURL" /* Variable Name */, "\"test.seoul.go.kr\"" /* Variable Value */ )
        }
        release {
            buildConfigField("String", "MYURL", "\"seoul.go.kr\"")
            /* Delcare for Release */
            signingConfig signingConfigs.release
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
        debug2{
        
        }
    }
}
```

And then you can use simply **BuildConfig** class static variable.

```
BuildConfig.APPLICATION_ID
BuildConfig.MYURL
```

## Release APK Run,Compile and Generate
 
 Before release version compiled you need belows.
  * keystore
  * signingConfigs in build.gradle

### Keystore
1. menu > build > generate signed key

2. If you don't have key store, make key store(It is needed one and once)

    2.1 If you have key store, just type key store password

3. Input key alias, key password. It's belong to Project

    3.1 Finish all above instruction, you have 'app-release.apk' in the app folder

4. Don't forget Sync Gradle

### Declare signingConfigs

Register **signingConfigs** in the **build.gradle** file

```
android {
    /* Declare Directly */
    signingConfigs {
        release{
            storeFile file("../../keystore/keystore.jks")   // Keystore Path
            storePassword "************"
            keyAlias "testKey"
            keyPassword "123456"
        }
    }
}
```

But this way has insecure problem. If you share this project to repository. Your key store information has exposed.
It can be solved using move that information to **gradle.properties** and **.gitignore**  

Note : It is ignored git repositry, you have to set **gradle.properties** manually.
unless it can't be worked properly.

1. Move information to gradle.properties

    ```
    # Project-wide Gradle settings.
    
    # IDE (e.g. Android Studio) users:
    # Gradle settings configured through the IDE *will override*
    # any settings specified in this file.
    
    # For more details on how to configure your build environment visit
    # http://www.gradle.org/docs/current/userguide/build_environment.html
    
    # Specifies the JVM arguments used for the daemon process.
    # The setting is particularly useful for tweaking memory settings.
    org.gradle.jvmargs=-Xmx1536m
    
    # When configured, Gradle will run in incubating parallel mode.
    # This option should only be used with decoupled projects. More details, visit
    # http://www.gradle.org/docs/current/userguide/multi_project_builds.html#sec:decoupled_projects
    # org.gradle.parallel=true
    
    storePw = *********
    keyId = testKey
    keyPw = 123456
    ```

2. Change delcare in **siningConfigs** File
    ```
        storePassword storePw
        keyAlias keyId
        keyPassword keyPw
    ```

3. add 'gradle.properties' file to '.gitignore'
    ```
        /gradle.properties
    ```
 
#### Compile,Run and Generate APK
* Compile, Run

    Build Variants is left side in Android Studio. You can change version and compile.

* Generate APK File

    Menu > Generate signed Apk

