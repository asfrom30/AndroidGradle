#Gradle Example

-. Two build.gradle files are existed in Project File
	: One is in the root, One is in the App folder

-. How can you use different Variable Value in each release and debug mode using Gradle

1. Declare Variable in the build.gradle file which is in the app folder
cf)
'''
debug{
	buildConfigField("String", "MYURL", "\"test.seoul.go.kr\"")
} release {
	buildConfigField("String", "MYURL", "\"seoul.go.kr\"")
}
'''

If you want to access Variable Value, Use BuildConfig Class
cf) BuildConfig.MYURL