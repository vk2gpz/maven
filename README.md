# vk2gpz Maven repository

Public Maven repository served by GitHub Pages at **https://repo.vk2gpz.com**.

| Path | Contents |
|---|---|
| `releases/` | Release versions |
| `snapshots/` | `-SNAPSHOT` versions |

## Using it

```kotlin
repositories {
    maven { url = uri("https://repo.vk2gpz.com/releases") }
    maven { url = uri("https://repo.vk2gpz.com/snapshots") } // only if you need snapshots
}
```

## Publishing to it

In the library's build, publish to a local clone of this repo, then commit and push:

```kotlin
publishing {
    repositories {
        maven {
            name = "vk2gpzPublic"
            val base = file(System.getProperty("user.home") + "/Code/maven")
            url = uri(if (version.toString().endsWith("SNAPSHOT")) base.resolve("snapshots") else base.resolve("releases"))
        }
    }
}
```

```sh
./gradlew publishAllPublicationsToVk2gpzPublicRepository
cd ~/Code/maven && git add -A && git commit -m "Publish <artifact> <version>" && git push
```

Private artifacts are not published here; they go to GitHub Packages on their own (private) repos.
