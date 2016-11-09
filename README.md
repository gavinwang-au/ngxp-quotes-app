# NGXP Quotes App
Quotes application for Web and Mobile (Android, iOS) with single code base buit with Angular and Nativescript.

## Previews and Screenshots
You can check previews and screenshots of this application for Web, Android and iOS platforms at [ngxp.io](http://ngxp.io/product/quotes-application/) 

## Prerequisites
1. Globally installed Nativecript  - `npm install -g nativescript`
2. Globally installed Angular CLI - `npm install -g angular-cli`
3. Mac OS to build iOS app.

## Installation
1. `git clone https://github.com/shripalsoni04/ngxp-quotes-app.git`
2. `cd ngxp-quotes-app`
3. `npm run ngxp-install`
    - As we are using nativescript-firebase plugin, just press **y** for below two questions when asked while installation. 
      - are you using iOS?
      - are you using android?
      - For all other questions press **n**. 

## Run Web application
`npm start` - This will start the application at http://localhost:4200. 

## Run iOS Application
- First start the simulator or connect the iOS device.
- Execute `npm run start.ios` 
- **Note** - If you are using XCode8 then you need to set the DEVELPMENT_TEAM. There are two ways to set it.
  1. Using XCode
      - After executing `npm run start.ios` command, open project wordspace file nativescript/platforms/ios/nativescript.xcworkspace in XCode
      - Click on nativescript project in XCode and set Team from General Tab.
      - The issue with thie approach is, you need to set it everytime you remove and add the iOS platform.
  2. From build.xconfig (preferable)
      - Open nativescript/app/App_Resources/iOS/build.xconfig file.
      - Uncomment `DEVELOPMENT_TEAM = YOUR_TEAM_ID;` line, and enter your team id.

## Run Android Application
- As we are using nativescript firebase plugin in the project, we need to perform below two steps before starting app on android.
  1. Copy `nativescript/app/App_Resources/Android/google-services.json` to `platforms/android` folder.
  2. Changes in `nativescript/platforms/android/build.gradle` file.
  
      Near the top there's a dependencies section, add classpath "com.google.gms:google-services:3.0.0" so it becomes something like:

      ```
      dependencies {
        classpath "com.android.tools.build:gradle:X.X.X"
        classpath "com.google.gms:google-services:3.0.0"
      }
      ```

      At the very bottom of the same file add
      
      ```
      apply plugin: "com.google.gms.google-services"
      ```
  3. Now execute `npm run start.android`
  
## Commands
You can execute any valid command of angular-cli from `web/` folder and any valid command of nativescript-cli from `nativescript/` folder.
For convenince below are the commands which you can execute from root directory.

### Common
| Command                | Description                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| npm run ngxp-install   | Installs dependencies of web and nativescript applications. Creates symlink of x-shared folder in both web and nativescript project. |

### Web Application
| Command                | Description                                                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| npm start              | Starts web application at http://localhost:4200                                                                                    |
| npm run start.prod     | Starts web application in production mode. Runs uglification and minification.                                                     |
| npm run start.aot      | Performs AOT for web application templates and starts web application. (Before executing this command refer Point 1 of [Known Issues](https://github.com/shripalsoni04/ngxp-quotes-app#known-issues-and-solution))                                                            |
| npm run start.aot.prod | Performs AOT, minification, uglification and starts web application. (Before executing this command refer Point 1 of [Known Issues](https://github.com/shripalsoni04/ngxp-quotes-app#known-issues-and-solution))                                                              |
| npm run build          | Builds the web application and copy the built project in web/dist folder.                                                          |
| npm run build.prod     | Builds the web application in production mode and copy the built project in web/dist folder.                                       |
| npm run build.aot      | Performs AOT, build the project and then copy the built project in web/dist folder.                                                |
| npm run build.aot.prod | Performs AOT, prepares production build and then copy the built project in web/dist folder.                                        |
| npm test               | Runs web application and x-shared unit test cases. It will not generate code coverage report.                                      |
| npm run test-cc        | Runs web application and x-shared unit test cases and generates code coverage report.                                              |
                                      

### Nativescript Application
| Command                  | Description                                                                                                                        |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| npm run start.ios        | Runs application on iOS emulator/device                                                                                            |
| npm run start.android    | Runs application on Android emulator/device                                                                                        |
| npm run livesync.ios     | Starts application in livesync mode on iOS emulator/device.                                                                        |
| npm run livesync.android | Starts application in livesync mode on Android emulator/device.       

## Known Issues and Solution
1. Regarding AOT
  - When you prepare aot build or serve project in aot mode, make sure you comment the exclude configuration in web/src/tsconfig.json file. Because currently AOT build also trying to compile test files and failing .This is know issue and can be tracked at https://github.com/angular/angular-cli/issues/2736. Once it is resolved, we can keep this uncommented for better unit testing support.
  ```
  // "exclude": [
  //   "**/*.spec.ts",
  //   "testing/**/*.ts"
  // ]
  ```

  - **Note**: When you execute `npm test` or `npm run test-cc` commands, make sure you uncomment above lines, otherwise test cases will give errors.

2. Angular dependencies at two levels for AOT support
  - Currently we have added angular dependencies in root level package.json and web/package.json. Because, AOT does not work properly when we use path mapping and this issue is reported and can be traked at https://github.com/angular/angular-cli/issues/1732 and PR:https://github.com/angular/angular-cli/pull/2470. Once this issue is resolved we can add path mapping as shown below and remove the angular dependencies from web/package.json, so in case of any version update we just need to change the version at root directory level.

    **web/src/tsconfig.json**
    ```
    "paths": {
        "@angular/*": ["../../node_modules/@angular/*"]
      }
    ```
   
## Attributes (All are npm packages)
1. nativescript-cardview
2. nativescript-floatingactionbutton
3. nativescript-iqkeyboardmanager
4. nativescript-material-icons
5. nativescript-ng2-fonticon
6. nativescript-plugin-firebase
7. nativescript-social-share
8. nativescript-swiss-army-knife
9. nativescript-theme-core
10. angular2-mdl
11. Awesome framework and toolchain of Nativescript and Angular.

## Coming Soon
- A starter project to quickly create your own cross platform application for web and native mobile platform similar to this application.
- A blog post explaining the folder structure of this application.
