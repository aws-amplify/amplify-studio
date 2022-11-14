# Amplify Storage

## Store user files on AWS, powered by Amazon S3.

[Image](https://raw.githubusercontent.com/aws-amplify/amplify-adminui/feat/sandbox-v2/markdown/categories/storage/img.png)

:::DESCRIPTION:::
Amplify Storage offers a simple mechanism for managing user-created content and app data. Store photos, audio, and video files for your app on device or in public, protected, or private storage modules in the cloud. Leverage cloud scale storage so that you can easily take your application from prototype to production.
:::DESCRIPTION_END:::


:::KEY_FEATURES:::
1. User file storage
2. File management
3. Event driven actions
:::KEY_FEATURES_END:::

:::VIDEO_WALKTHROUGH:::
https://www.youtube-nocookie.com/embed/Be0hmfNMdxI
:::VIDEO_WALKTHROUGH_END:::

    // Amplify plugins
    implementation 'com.amplifyframework:core:2.0.0'
    implementation 'com.amplifyframework:aws-api:2.0.0'
    implementation 'com.amplifyframework:aws-datastore:2.0.0'

    // Support for Java 8 features
    coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:1.0.10'