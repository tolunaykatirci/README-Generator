# Cordova Plugin HMS Nearby

## Contents

- [1. Introduction](#1-introduction)
- [2. Installation Guide](#2-installation-guide)
  - [2.1. Creating a Project in AppGallery Connect](#21-creating-a-project-in-appgallery-connect)
  - [2.2. Configuring the Signing Certificate Fingerprint and Obtaining agconnect-services.json](#22-configuring-the-signing-certificate-fingerprint-and-obtaining-agconnect-servicesjson)
  - [2.3. Cordova](#23-cordova)
  - [2.4. Ionic](#24-ionic)
    - [2.4.1. With Cordova Runtime](#241-with-cordova-runtime)
    - [2.4.2. With Capacitor Runtime](#242-with-capacitor-runtime)
- [3. API Reference](#3-api-reference)
  - [3.1. Functions Overview](#31-functions-overview)
    - [3.1.1. Public Methods](#311-public-methods)
- [4. Configuration and Description](#4-configuration-and-description)
- [5. Sample Project](#5-sample-project)
- [6. Questions or Issues](#6-questions-or-issues)
- [7. Licencing and Terms](#7-licencing-and-terms)

---

## 1. Introduction

This plugin enables communication between Huawei Nearby SDK and Cordova platform. It exposes all functionality provided by Huawei Nearby SDK.

---

## 2. Installation Guide

Before you get started, you must register as a HUAWEI Developer and complete identity verification on the [HUAWEI Developer](https://developer.huawei.com/consumer/en/) website. For details, please refer to [Register a HUAWEI ID](https://developer.huawei.com/consumer/en/doc/10104).

### 2.1. Creating a Project in AppGallery Connect

Creating an app in AppGallery Connect is required in order to communicate with the Huawei services. To create an app, perform the following steps:

1. Sign in to [AppGallery Connect](https://developer.huawei.com/consumer/en/service/josp/agc/index.html)  and select **My projects**.
2. Select your project from the project list or create a new one by clicking the **Add Project** button.
3. Go to **Project Setting** > **General information**, and click **Add app**.
If an app exists in the project and you need to add a new one, expand the app selection area on the top of the page and click **Add app**.
4. On the **Add app** page, enter the app information, and click **OK**.

### 2.2. Configuring the Signing Certificate Fingerprint and Obtaining agconnect-services.json

A signing certificate fingerprint is used to verify the authenticity of an app when it attempts to access an HMS Core (APK) through the HMS SDK. Before using the HMS Core (APK), you must locally generate a signing certificate fingerprint and configure it in the **AppGallery Connect**. You can refer to 3rd and 4th steps of [Generating a Signing Certificate](https://developer.huawei.com/consumer/en/codelab/HMSPreparation/index.html#2) Codelab tutorial for the certificate generation. Perform the following steps after you have generated the certificate.

1. Sign in to [AppGallery Connect](https://developer.huawei.com/consumer/en/service/josp/agc/index.html) and select your project from **My Projects**. Then go to **Project Setting** > **General information**. In the **App information** field, click the  icon next to SHA-256 certificate fingerprint, and enter the obtained **SHA-256 certificate fingerprint**.
2. After completing the configuration, click **OK** to save the changes. (Check mark icon)
3. In the same page, click **agconnect-services.json** button to download the configuration file.

### 2.3. Cordova

1. Install Cordova CLI.

    ```bash
    npm install -g cordova
    ```

2. Create a new Cordova project or use existing Cordova project.

    - To create new Cordova project, you can use **`cordova create path [id [name [config]]] [options]`** command. For more details please follow [CLI Reference - Apache Cordova](https://cordova.apache.org/docs/en/latest/reference/cordova-cli/index.html#cordova-create-command).

3. Update the widget **`id`** property which is specified in the **`config.xml`** file. It must be same with **client > package_name** value of the **`agconnect-services.json`** file.

4. Add the **Android platform** to the project if haven't done before.

    ```bash
    cordova platform add android
    ```

5. Install `HMS Nearby plugin` to the project. You can either install the plugin through `npm` or by `downloading from HMS Core Plugin page`.

    a. Run the following command in the root directory of your project to install it through **npm**.

    ```bash
    cordova plugin add @hmscore/cordova-plugin-hms-nearby
    ```

    b. Or download the plugin from [Plugin > Nearby Kit > Cordova Plugin](https://developer.huawei.com/consumer/en/doc/overview/HMS-Core-Plugin) page and run the following command in the root directory of your project to **install it manually**.

    ```bash
    cordova plugin add <hms_cordova_nearby_plugin_path>
    ```

6. Copy **`agconnect-services.json`** file to **`<project_root>/platforms/android/app`** directory.

7. Add **`keystore(.jks)`** and **`build.json`** files to your project's root directory.

    - You can refer to 3rd and 4th steps of [Generating a Signing Certificate](https://developer.huawei.com/consumer/en/codelab/HMSPreparation/index.html#2) Codelab tutorial page for generating keystore file.
    - Fill **`build.json`** file according to your keystore information. For example:

    ```json
    {
        "android": {
            "debug": {
                "keystore": "<keystore_file>.jks",
                "storePassword": "<keystore_password>",
                "alias": "<key_alias>",
                "password": "<key_password>"
            },
            "release": {
                "keystore": "<keystore_file>.jks",
                "storePassword": "<keystore_password>",
                "alias": "<key_alias>",
                "password": "<key_password>"
            }
        }
    }
    ```

8. Run the application.

    ```bash
    cordova run android --device
    ```

---

### 2.4. Ionic

1. Install Ionic CLI.

    ```bash
    npm install -g @ionic/cli
    ```

2. Create a new Ionic project or use existing Ionic project.

    - To create a new Ionic project, you can use **`ionic start <name> <template> [options]`** command. For more details please follow [ionic start - Ionic Documentation](https://ionicframework.com/docs/cli/commands/start).

#### 2.4.1. With Cordova Runtime

1. Enable the **Cordova integration** if haven't done before.

    ```bash
    ionic integrations enable cordova
    ```

2. Update the widget **`id`** property which is specified in the **`config.xml`** file. It must be same with **client > package_name** value of the **`agconnect-services.json`** file.

3. Add the **Android platform** to the project if haven't done before.

    ```bash
    ionic cordova platform add android
    ```

4. Install `HMS Nearby plugin` to the project. You can either install the plugin through `npm` or by `downloading from HMS Core Plugin page`.

    a. Run the following command in the root directory of your project to install it through **npm**.

    ```bash
    ionic cordova plugin add @hmscore/cordova-plugin-hms-nearby
    ```

    b. Or download the plugin from [Plugin > Nearby Kit > Cordova Plugin](https://developer.huawei.com/consumer/en/doc/overview/HMS-Core-Plugin) page and run the following command in the root directory of your project to **install it manually**.

    ```bash
    ionic cordova plugin add <hms_cordova_nearby_plugin_path>
    ```

5. Copy **hms-nearby** folder from **`node_modules/@hmscore/cordova-plugin-hms-nearby/ionic/wrapper/dist`** directory to **`node_modules/@ionic-native`** directory.

6. Copy **`agconnect-services.json`** file to **`<project_root>/platforms/android/app`** directory.

7. Add **`keystore(.jks)`** and **`build.json`** files to your project's root directory.

    - You can refer to 3rd and 4th steps of [Generating a Signing Certificate](https://developer.huawei.com/consumer/en/codelab/HMSPreparation/index.html#2) Codelab tutorial page for generating keystore file.

    - Fill **`build.json`** file according to your keystore information. For example:

    ```json
    {
        "android": {
            "debug": {
                "keystore": "<keystore_file>.jks",
                "storePassword": "<keystore_password>",
                "alias": "<key_alias>",
                "password": "<key_password>"
            },
            "release": {
                "keystore": "<keystore_file>.jks",
                "storePassword": "<keystore_password>",
                "alias": "<key_alias>",
                "password": "<key_password>"
            }
        }
    }
    ```

8. Run the application.

   ```bash
   ionic cordova run android --device
   ```

#### 2.4.2. With Capacitor Runtime

1. Enable the **Capacitor integration** if haven't done before.

   ```bash
   ionic integrations enable capacitor
   ```

2. Update the widget **`appId`** property which is specified in the **`capacitor.config.json`** file. It must be same with **client > package_name** value of the **`agconnect-services.json`** file.

3. Install `HMS Nearby plugin` to the project. You can either install the plugin through `npm` or by `downloading from HMS Core Plugin page`.

   a. Run the following command in the root directory of your project to install it through **npm**.

    ```bash
    npm install @hmscore/cordova-plugin-hms-nearby
    ```

   b. Or download the plugin from [Plugin > Nearby Kit > Cordova Plugin](https://developer.huawei.com/consumer/en/doc/overview/HMS-Core-Plugin) page and run the following command in the root directory of your project to **install it manually**.

    ```bash
    npm install <hms_cordova_nearby_plugin_path>
    ```

4. Copy **hms-nearby** folder from **`node_modules/@hmscore/cordova-plugin-hms-nearby/ionic/wrapper/dist`** directory to **`node_modules/@ionic-native`** directory.

5. Build Ionic app to generate resource files.

    ```bash
    ionic build
    ```

6. Add the **Android platform** to the project if haven't done before.

    ```bash
    npx cap add android
    ```

7. Copy **`keystore(.jks)`** and **`agconnect-services.json`** files to **`<project_root>/android/app`** directory.

    - You can refer to 3rd and 4th steps of [Generating a Signing Certificate](https://developer.huawei.com/consumer/en/codelab/HMSPreparation/index.html#2) Codelab tutorial page for generating keystore file.

8. Open the **`build.gradle`** file in the **`<project_root>/android/app`** directory.

    - Add `signingConfigs` entry to **android** according to your keystore information.
    - Enable `signingConfig` configuration to **debug** and **release** flavors.
    - Apply `com.huawei.agconnect` plugin.

    ```groovy
    ...

    android {

        ...

        // Add signingConfigs according to your keystore information
        signingConfigs {
            config {
                storeFile file('<keystore_file>.jks')
                storePassword '<keystore_password>'
                keyAlias '<key_alias>'
                keyPassword '<key_password>'
            }
        }
        buildTypes {
            debug {
                signingConfig signingConfigs.config // Enable signingConfig in debug flavor
            }
            release {
                signingConfig signingConfigs.config // Enable signingConfig in release flavor
                minifyEnabled false
                proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            }
        }
    }

    ...

    apply plugin: 'com.huawei.agconnect' // Apply com.huawei.agconnect plugin. This line must be added to the end of the file.
    ```

9. Open the **`build.gradle`** file in the **`<project_root>/android`** directory. Add **Huawei's maven repositories** and **agconnect classpath** to the file.

    ```groovy
    buildscript {
        repositories {
            /*
                <Other repositories>
            */
            maven { url 'https://developer.huawei.com/repo/' }
        }
        dependencies {
            /*
                <Other dependencies>
            */
            classpath 'com.huawei.agconnect:agcp:1.4.1.300'
        }
    }

    /*
        <Other build.gradle entries>
    */

    allprojects {
        repositories {
            /*
                <Other repositories>
            */
            maven { url 'https://developer.huawei.com/repo/' }
        }
    }
    ```

10. Open the project in Android Studio and run it.

    ```bash
    npx cap open android
    ```


---

## 3. API Reference
### FunctionParameter
|Field|Type|Description|
|---|---|---|
|key|`string`| |
|value|`string`| |
|defaultValue?|`string`| |

### TypeFunction
#### Public Method Summary
|Method|Return Type|Description|
|---|---|---|
|constructor(functionName:  string)|`any`| |
#### Public Methods

##### constructor(functionName: string)
null
###### Parameters
|Name|Type|Description|
|---|---|---|
|functionName| string|null|
###### Return Type
|Type|Description|
|---|---|
|`any`|null|
###### Call Example
```ts
function constructor() {
	try {
		const functionName = 'todo';
		HMSNearby.constructor(functionName);
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```



### ClassFunction
#### Public Method Summary
|Method|Return Type|Description|
|---|---|---|
|constructor(functionName:  string)|`any`| |
#### Public Methods

##### constructor(functionName: string)
null
###### Parameters
|Name|Type|Description|
|---|---|---|
|functionName| string|null|
###### Return Type
|Type|Description|
|---|---|
|`any`|null|
###### Call Example
```ts
function constructor() {
	try {
		const functionName = 'todo';
		HMSNearby.constructor(functionName);
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```



### ClassVariables
#### Public Method Summary
|Method|Return Type|Description|
|---|---|---|
#### Public Methods



### Enum AccessSpecifier
|Field|Value|Description|
|---|---|---|
|PRIVATE|"PRIVATE"| |
|PUBLIC|"PUBLIC"| |
|PROTECTED|"PROTECTED"| |
|DEFAULT|""| |

### TypeClass
#### Public Method Summary
|Method|Return Type|Description|
|---|---|---|
|constructor(className:  string,  abstract:  boolean)|`any`| |
|addFunction(funcName:  string,  parameters:  string,  returnType:  string,  accessSpecifier:  AccessSpecifier)|`any`| |
|addVariable()|`any`| |
|getVariables()|`ClassVariables[]`| |
#### Public Methods

##### constructor(className: string,  abstract: boolean)
null
###### Parameters
|Name|Type|Description|
|---|---|---|
|className| string|null|
|  abstract| boolean|null|
###### Return Type
|Type|Description|
|---|---|
|`any`|null|
###### Call Example
```ts
function constructor() {
	try {
		const className = 'todo';
		const abstract = 'todo';
		HMSNearby.constructor(className, abstract);
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```

##### addFunction(funcName: string,  parameters: string,  returnType: string,  accessSpecifier: AccessSpecifier)
Function description.
###### Parameters
|Name|Type|Description|
|---|---|---|
|funcName| string|Param description.|
|  parameters| string|Param description.|
|  returnType| string|Param description.|
|  accessSpecifier| AccessSpecifier|Param description.|
###### Return Type
|Type|Description|
|---|---|
|`any`|null|
###### Call Example
```ts
function addFunction() {
	try {
		const funcName = 'todo';
		const parameters = 'todo';
		const returnType = 'todo';
		const accessSpecifier = 'todo';
		HMSNearby.addFunction(funcName, parameters, returnType, accessSpecifier);
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```

##### addVariable()
null
###### Return Type
|Type|Description|
|---|---|
|`any`|null|
###### Call Example
```ts
function addVariable() {
	try {
		HMSNearby.addVariable();
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```

##### getVariables()
null
###### Return Type
|Type|Description|
|---|---|
|`ClassVariables[]`|null|
###### Call Example
```ts
function getVariables() {
	try {
		HMSNearby.getVariables();
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```

##### getFunctions()
null
###### Return Type
|Type|Description|
|---|---|
|`ClassFunction[]`|null|
###### Call Example
```ts
function getFunctions() {
	try {
		HMSNearby.getFunctions();
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```



### Public Method Summary
|Method|Return Type|Description|
|---|---|---|
|test()|`any`|null|
|sample(sample:string)|`Promise<string>`|Function description.|
#### Public Methods

##### test()
null
###### Return Type
|Type|Description|
|---|---|
|`any`|null|
###### Call Example
```ts
function test() {
	try {
		HMSNearby.test();
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```

##### sample(sample:string)
Function description.
###### Parameters
|Name|Type|Description|
|---|---|---|
|sample|string|Param description.|
###### Return Type
|Type|Description|
|---|---|
|`Promise<string>`|Return description.|
###### Call Example
```ts
async function sample() {
	try {
		const sample = 'todo';
		await HMSNearby.sample(sample);
	} catch(ex) {
		alert(JSON.stringify(ex));
	}
}
```



---


## 4. Configuration and Description

No

---

## 5. Sample Project

You can find the sample projects on [HMS Core > Examples > Nearby Kit](https://developer.huawei.com/consumer/en/doc/overview/HMS-Core-Plugin) page.

---

## 6. Questions or Issues

If you have questions about how to use HMS samples, try the following options:

- [Stack Overflow](https://stackoverflow.com/questions/tagged/huawei-mobile-services) is the best place for any programming questions. Be sure to tag your question with **`huawei-mobile-services`**.
- [GitHub](https://github.com/HMS-Core/hms-cordova-plugin) is the official repository for these plugins, You can open an issue or submit your ideas.
- [Huawei Developer Forum](https://forums.developer.huawei.com/forumPortal/en/home?fid=0101187876626530001) HMS Core Module is great for general questions, or seeking recommendations and opinions.
- [Huawei Developer Docs](https://developer.huawei.com/consumer/en/doc/overview/HMS-Core-Plugin) is place to official documentation for all HMS Core Kits, you can find detailed documentations in there.

If you run into a bug in our samples, please submit an issue to the [GitHub repository](https://github.com/HMS-Core/hms-cordova-plugin).

---

## 7. Licencing and Terms

Huawei Nearby Kit Cordova Plugin is licensed under the [Apache 2.0 license](LICENCE).