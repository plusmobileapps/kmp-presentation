#### Gradle build.gradle.kts

```gradle [8|15|18|20-24|26-32|33-35|37-40|42-44|46-48|51-56]
buildscript {
  repositories {
        google()
        jcenter()
        mavenCentral()
  }
  dependencies {
    classpath("com.squareup.sqldelight:gradle-plugin:1.5.0")
  }
}

plugins {
    kotlin("multiplatform")
    id("com.android.library")
    id("com.squareup.sqldelight")
}

kotlin {
    //select iOS target platform depending on the Xcode environment variables
    val iOSTarget: (String, KotlinNativeTarget.() -> Unit) -> KotlinNativeTarget =
        if (System.getenv("SDK_NAME")?.startsWith("iphoneos") == true)
            ::iosArm64
        else
            ::iosX64

    iOSTarget("ios") {
        binaries {
            framework {
                baseName = "SharedCode"
            }
        }
    }
    targets {
        android()
    }

    sourceSets["commonMain"].dependencies {
        implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.0")
        implementation("com.squareup.sqldelight:runtime:1.5.0")
    }

    sourceSets["androidMain"].dependencies {
        implementation("com.squareup.sqldelight:android-driver:1.5.0")
    }

    sourceSets["iosMain"].dependencies {
        implementation("com.squareup.sqldelight:native-driver:1.5.0")
    }
}

sqldelight {
    database("MyDatabase") { // This will be the name of the generated database class.
        packageName = "com.plusmobileapps.sharedcode.db"
        sourceFolders = listOf("sqldelight")
    }
}
```