
👋 Welcome! In this tutorial, you will:

- Create an Android application configured with Amplify
- Use Amplify DataStore to model and persist data
- Connect your local data to synchronize to a cloud backend

## Prerequisites

  <amplify-callout warning>

  **KNOWN LIMITATION** This tutorial currently does not work under Windows.

  </amplify-callout>

- Install [Node.js](https://nodejs.org/en/) version 10 or higher
- Install [Android Studio](https://developer.android.com/studio/index.html#downloads) version 3.6 or higher
- Install the [Android SDK](https://developer.android.com/studio/releases/platforms) API level 16 (Jelly Bean) or higher
- Install the latest version of the [Amplify CLI](~/cli/cli.md) by running:

    ```bash
    npm install -g @aws-amplify/cli
    ```

## Configure your application

1. Create a new Android application in **Android Studio**. If you are new to Android development, you can follow [these steps](https://developer.android.com/training/basics/firstapp/creating-project) in the Android documentation to create a new project in either Java or Kotlin.

1. Open your **project** `build.gradle` and add the following:
    - `mavenCentral()` in the `repositories` block
    - `classpath 'com.amplifyframework:amplify-tools-gradle-plugin:0.2.1'` in the `dependencies` block
    - Apply the plugin `'com.amplifyframework.amplifytools'` 

    Note you will need to add the above three items in the right sections, for example:

    ```groovy
    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath 'com.amplifyframework:amplify-tools-gradle-plugin:0.2.1'
        }
    }

    apply plugin: 'com.amplifyframework.amplifytools'

1. Open your **app** `build.gradle` and add the following:
    - `sourceCompatibility` and `targetCompatibility` to Java 1.8; this allows your application to make use of Java 8 features like Lambda expressions
    - Add Amplify Core and DataStore libraries in the `dependencies` block

    ```groovy
    android {
        compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_8
            targetCompatibility JavaVersion.VERSION_1_8
        }
    }

    dependencies {
        implementation 'com.amplifyframework:core:0.10.0'
        implementation 'com.amplifyframework:aws-datastore:0.10.0'
        implementation 'com.amplifyframework:aws-apii:0.10.0'
    }
    ```

1. Run **Make Project**

    When the build is successful, two new Gradle tasks will be added to your project - `modelgen` and `amplifyPush`. In the Android Studio, you'll find these tasks in the top bar in a dropdown menu. Look for a drop-down menu displaying the word "app", if it's a new project.

    <amplify-callout>

    **HELP** If you get the following error message: `ERROR: Process 'command 'npx'' finished with non-zero exit value 1`, this may be due to the logged in user on your machine having insufficient permissions to access the `node_modules` folder on your machine. Follow [these steps](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) to resolve it.

    </amplify-callout>