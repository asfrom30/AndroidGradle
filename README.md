# Gradle Example

-. Two build.gradle files are existed in Project File
	: One is in the root, One is in the App folder

## How can you use different Variable Value in each release and debug mode using Gradle

1. Declare Variable in the build.gradle file which is in the app folder
cf) below code block means 'public static final String MYURL = test.seoul.go.kr' or seoul.go.kr in the BuildConfig.java class
'''
debug{
	buildConfigField("String", "MYURL", "\"test.seoul.go.kr\"")
} release {
	buildConfigField("String", "MYURL", "\"seoul.go.kr\"")
}
'''

2. It means you can change variable value in Debug and Release Build without typing

3. If you want to access Variable Value, Use BuildConfig Class
cf) BuildConfig.MYURL


[lecture pdf file](https://github.com/asfrom30/GradleSetting/blob/master/002_Builder_Gradle.pdf)

## How can you create and test Debug and Release version apk
1. menu > build > generate signed key

2. If you don't have key store, make key store(It is needed one and once)
2.1 If you have key store, just type key store password

3. Input key alias, key password. It's belong to Project
3.1 Finish all above instruction, you have 'app-release.apk' in the app folder

4. Don't forget Sync Gradle

5. Register 'signingConfigs' in the 'build.gradle' file
    signingConfigs {
        release{
            // It is insecure.
            storeFile file("../../keystore/keystore.jks")   // notify keystore's path
            storePassword "123456"
            keyAlias "testKey"
            keyPassword "123456"
        }
    }

5.1 If you don't want to expose your keyAlias and key password
5.2 Move storePassword, keyAlias, keyPassword to 'gradle.properties' in root directory
```
cf)
	storePw ="123456"
	keyId="testKey"
	keyPw="123456"
```

5.3 Change siningConfigs File
```
cf)
	storePassword storePw
	keyAlias keyId
	keyPassword keyPw
```
5.4 add 'gradle.properties' file to '.gitignore'
```
cf)
	/gradle.properties
```
