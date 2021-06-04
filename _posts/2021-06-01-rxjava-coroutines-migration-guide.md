# RxJava2 to Coroutines Migration Guide

```kotlin val coroutinesVersion = "1.5.0"

dependencies { 
  implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm:$coroutinesVersion")
  implementation("org.jetbrains.kotlinx:kotlinx-coroutines-reactive:$coroutinesVersion")
  implementation("org.jetbrains.kotlinx:kotlinx-coroutines-reactor:$coroutinesVersion")
  implementation("org.jetbrains.kotlinx:kotlinx-coroutines-rx3:$coroutinesVersion")
  ...
}```