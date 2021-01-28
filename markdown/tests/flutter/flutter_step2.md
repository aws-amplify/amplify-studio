- Open **Android Studio** and select **+ Start a new Flutter project**.
- In **Select a Project Template**, select **Flutter Application**. Press Next.

- Next, configure your project:
  - Enter todo in the Name field
  - Make sure your Flutter SDK path is set correctly to where it is installed on your machine
  - Press Next. On the next screen, press Finish.

Lastly, modify your Podfile to target iOS platform 11.0 or higher. Within your project open ios/Podfile and change the second line to be `platform :ios, ‘11.0’.
