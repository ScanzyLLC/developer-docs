# Scanzy Barcode Scanner SDK Guideline - React Native

Scanzy Barcode Scanner SDK implements the barcode capture capabilities of the ScanzyBarcodeScannerSDK for mobile. It supports reading a large number of different barcode symbologies, such as Code39, Code93, Code128, Codabar, UPC-A, UPC-E, EAN-8, EAN-13, ITF, QRCode, Aztec, PDF-417, Data Matrix, etc.


Before you started, get a 14 days free trial License Key from [scanzy.com](https://scanzy.com/trial).

Follow the instructions below to integrate the SDK into your app or check out the [sample](https://github.com/ScanzyLLC/ScanzyBarcodeScannerSDKSampleReactNative). If you have any questions or need help, check out official website [scanzy.com](https://scanzy.com).


## Prerequisites

- Install [Node.js](https://nodejs.org) which includes [Node Package Manager](https://www.npmjs.com/get-npm), version 14 or higher
- Android development: Install [Android Studio](https://developer.android.com/studio)
- iOS development: Install [XCode](https://apps.apple.com/de/app/xcode/id497799835?mt=12)
- ios development: Install [CocoaPods](https://guides.cocoapods.org/using/getting-started.html)
- This project uses [React Native](https://reactnative.dev/) as app development platform and the [npx].

## Installation

```sh
npm install react-native-scanzy-barcode-scanner-plugin
```

For an iOS project, in order to get camera permission, please add the below configs to the Info.plist of the Project Targets.
```xml
<key>NSCameraUsageDescription</key>
<string>camera description.</string>
```

For an Android project, add the following config in the same build.gradle(Android/app/build.gradle) file to avoid conflicts with the lib filename libc++_shared.so, which is used by React Native as well as by many other 3rd-party modules:
```
android {  
    ...  
    packagingOptions {      
        pickFirst '**/libc++_shared.so'  
    }
}
```

## Usage

```js
import ScanzyBarcodeManager, {ScanzyBarcodeFormat, ScanzyBarcodeOptions} from 'react-native-scanzy-barcode-scanner-plugin';

//set lisense in your app init function
ScanzyBarcodeManager.setLicense('YOUR LICENSE KEY');

//set scan formats and options
const formats = [ScanzyBarcodeFormat.Code128, ScanzyBarcodeFormat.Code93, ScanzyBarcodeFormat.EAN13, ScanzyBarcodeFormat.QRCode];
const options: ScanzyBarcodeOptions = {
  enableVibration: true,
  enableBeep: true,
  enableAutoZoom: false,
  enableScanCropRectOnly: false,
  formats: formats
}

// scan
ScanzyBarcodeManager.scan(options).then((result: ScanzyBarcodeScanResult)=>{
  //get the scan result
  console.log('Scan Result:', result.barcode, result.barcodeType)
})
```

## API Specification
Below are more details about the parameters:

The definition of <strong>ScanzyBarcodeFormat</strong>:
```typescript
const ScanzyBarcodeFormat = {
  Code128:"Code128",
  Code39:"Code39",
  Code93:"Code93",
  CodaBar:"CodaBar",
  DataMatrix:"DataMatrix",
  EAN13:"EAN13",
  EAN8:"EAN8",
  ITF:"ITF",
  QRCode:"QRCode",
  UPCA:"UPCA",
  UPCE:"UPCE",
  PDF417:"PDF417",
  Aztec:"Aztec",
  MaxiCode:"MaxiCode"
}

```
Note: Set only the formats you are interested in. You can add ALL formats, but it would impact performance.


The <strong>ScanzyBarcodeOptions</strong> is defined as:
```typescript
interface ScanzyBarcodeOptions {
  enableVibration?: boolean;
  enableBeep?: boolean;
  enableAutoZoom?: boolean;
  enableScanCropRectOnly?: boolean;
  formats?: string[];
}

```
|     Parameter    |   Description         | 
| ------------- |:-------------:| 
| enableVibration      | vibrate your phone when a barcode is detected |
| enableBeep      |   play a beep sound when a barcode is detected    |  
| enableAutoZoom |   the library will zoom in/out automatcially to scan a barcode    |   
| enableScanCropRectOnly |   only scan the view finder area    |   
| formats |   the barcode formats    |  


The <strong>ScanzyBarcodeScanResult</strong> is defined as:
```typescript
interface ScanzyBarcodeScanResult {
  barcode: string;
  barcodeType: string;
}
```
