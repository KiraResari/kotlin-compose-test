# 19-Dec-2022

* This is about evaluating Kotlin Compose

* I found this for reading up on it:

  * https://simply-how.com/getting-started-with-compose-for-desktop

  * It says I need IntelliJ for this, but let's see if Android Studio will also work

    * At first look it seems like it works, but I'll brace myself for complications further down the line
    * Aaand, it looks like it's doing the 10-minute gradle download thing again, which I suppose is okay since this is a new project (I downloaded the sample project template as instructed in the tutorial), and if that needs to happen once at the start of each new project, that's acceptable

  * So, the basic hello world desktop application from that works

  * However, the calculator app sample runs into issues

    * When I copy the code from the tutorial website, it has problems with

      * ````
        fun main() = Window(
        ````

      * Namely:

      * ````
        Functions which invoke @Composable functions must be marked with the @Composable annotation
        ````

      * And if I add `@Composable`, it changes to:

      * ````
        Composable main functions are not currently supported
        ````

      * It works if I do it like this...

      * ````
        fun main() = application {
            Window(
        ````

      * However, then more issues happen

      * I think this example might be broken

      * Let me check out the sample code and see

      * That one is located here:

        * https://github.com/soufianesakhi/compose-desktop-calculator
        * Aaaand, again, ten minute initial build time for the new project

      * Somehow, there it works

      * Maybe a different type of `Window` is used there

      * There, it is from `androidx.compose.desktop.Window`

        * I did try importing that, but it said it couldn't find it

        * Here it works just fine though

        * So maybe it's an issue with the gradle?

        * Yes, looks like they're still using an old version of compose where things apparently behave different enough to cause issues

          * ````kotlin
            plugins {
                kotlin("jvm") version "1.4.10"
                // __UPDATE_COMPOSE_VERSION_MARKER__
                id("org.jetbrains.compose") version (System.getenv("COMPOSE_TEMPLATE_COMPOSE_VERSION") ?: "0.1.0-build113")
            }
            ````

        * And what is the current version?

          * That would be 1.2.2

        * Ugh, so no wonder the tutorial doesn't work, if it was  for an indev version of Compose

  * Let me try to find a more recent Kotlin Compose tutorial
    * Maybe this will be good?
      * https://developer.android.com/jetpack/compose/tutorial
      * Hmm, not sure, that looks a lot like the Kotlin Multiplatform Thing, which _might_ be a good thing, but I don'T think it shows me how to write a desktop app
    * Maybe this is better?
      * https://github.com/JetBrains/compose-jb/blob/master/tutorials/Getting_Started/README.md
      * Okay, this does seem to work, but somehow it doesn't seem fit for Android
    * But here it says this can also be used for android development:
      * https://github.com/JetBrains/compose-jb
    * Hmm, maybe I can combine Compose and KMM after all in order to create a Multiplatform and Desktop experience?
      * It does annoy me, however, that "Multiplatform" never seems to include both Mobile and Desktop



# ⚓