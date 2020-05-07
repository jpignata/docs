
In this tutorial, you will:

- Create an Android application configured with Amplify
- Use DataStore to model and persist data
- Connect your local data to synchronize to a cloud backend

You will create a Todo app using Amplify DataStore as a local-only persistence mechanism. DataStore provides a programming model for storing data offline and online without writing additional code. 

## Prerequisites

  <amplify-callout warning>

  **KNOWN LIMITATION** This tutorial currently does not work under Windows.

  </amplify-callout>

- [Install Node.js](https://nodejs.org/en/) version 10 or higher
- [Install Android Studio](https://developer.android.com/studio/index.html#downloads) version 3.6 or higher
- [Install Android SDK](https://developer.android.com/studio/releases/platforms) with a minimum API level of 16 (Jelly Bean)
- Create a new Android application. If you are new to Android development, you can follow [these steps](https://developer.android.com/training/basics/firstapp/creating-project)
- Install the latest version of the Amplify CLI by running:

    ```bash
    npm install -g @aws-amplify/cli
    ```

## Configure your application

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

    When the build is successful, it will add two Gradle tasks to you project - `modelgen` and `amplifyPush`. (In the Android Studio UI, these tasks can be found in the top bar, up where you would run your project. Look for a drop-down menu displaying the word "app", if it's a new project.)

    <amplify-callout>

    **HELP** If you get the following error message: `ERROR: Process 'command 'npx'' finished with non-zero exit value 1`, this may be due to the logged in user on your machine having insufficient permissions to access the `node_modules` folder on your machine. Follow [these steps](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) to resolve it.

    </amplify-callout>