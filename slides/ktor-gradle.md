#### Ktor build.gradle.kts

```kotlin [3|7|8-9|12|15|18]
plugins {
    kotlin("multiplatform")
    kotlin("plugin.serialization") version "1.5.0"
}

//common
implementation("io.ktor:ktor-client-core:$ktor_version")
implementation("io.ktor:ktor-client-serialization:$ktor_version")
implementation("org.jetbrains.kotlinx:kotlinx-serialization-json:$serialization_version")

//android
implementation("io.ktor:ktor-client-android:$ktor_version")

//iOS
implementation "io.ktor:ktor-client-ios:$ktor_version"

//js
implementation("io.ktor:ktor-client-js:$ktor_version")

```