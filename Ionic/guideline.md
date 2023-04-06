# Scanzy Barcode Scanner SDK Guideline - Ionic

Scanzy Barcode Scanner SDK implements the barcode capture capabilities of the ScanzyBarcodeScannerSDK for mobile. It supports reading a large number of different barcode symbologies, such as Code39, Code93, Code128, Codabar, UPC-A, UPC-E, EAN-8, EAN-13, ITF, QRCode, Aztec, PDF-417, Data Matrix, etc.

Before you started, get a 14 days free trial License Key from [scanzy.com](https://scanzy.com/trial).

Follow the instructions below to integrate the SDK into your app or check out the [sample](https://github.com/ScanzyLLC/scanzy-barcodescanner-sample-ionic-capacitor). If you have any questions or need help, check out official website [scanzy.com](https://scanzy.com).


## Prerequisites

- Install [Node.js v14](https://nodejs.org) or higher, with [Node Package Manager](https://www.npmjs.com/get-npm) v7.24 or higher
- Android development: Install [Android Studio](https://developer.android.com/studio)
- iOS development: Install [XCode](https://apps.apple.com/de/app/xcode/id497799835?mt=12)
- This project uses [Ionic](https://ionicframework.com/) as an app development platform and the [Ionic CLI](https://ionicframework.com/docs/cli).

## Installation

#### Install the plugin into the ionic cordova project

```npm
ionic cordova plugin add cordova-plugin-scanzy-barcodescanner --save
```

#### Or install the plugin into the ionic capacitor project

```npm
npm install cordova-plugin-scanzy-barcodescanner --save
ionic capacitor sync
```

## Quick Start

To use this plugin in Javascript:

First, set the license key you obtained from [Scanzy](https://scanzy.com) for free trial. It's better to do it in your app's startup, although it's fine to call this function every single time a barcode is scanned.


```javascript

 ScanzyBarcodeManager.setLicense("YOUR LICENSE KEY");

```

Then, insert the below code snippet into the place where you are scanning barcodes:

```javascript

  scan = function () {
    const barcodeFormats = [ScanzyBarcodeFormat.Code128,ScanzyBarcodeFormat.Code39];
    const barcodeOptions = new ScanzyBarcodeOptions(true, true, true, true, barcodeFormats);
    ScanzyBarcodeManager.scan(this.scanSuccess.bind(this), this.scanFailure.bind(this), barcodeOptions);
  }
  
  
  scanSuccess = function (result) {
    console.log('scan result:', result.barcode, result.barcodeType);
    //your actual business logic to deal with the returned barcode text and barcode type from ScanzyBarcodeScannerSDK
  };

  scanFailure = function (err) {
    //your actual business logic to deal with the returned error from ScanzyBarcodeScannerSDK
  };

```

## API Specification
More details about the parameters:

The definition of <strong>ScanzyBarcodeFormat</strong>:
```javascript
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

<strong>ScanzyBarcodeOptions</strong> is defined as:
```javascript
  function ScanzyBarcodeOptions(enableVibration, enableBeep, enableAutoZoom, enableScanCropRectOnly, formats) {
    this.enableVibration = enableVibration;
    this.enableBeep = enableBeep;
    this.enableAutoZoom = enableAutoZoom;
    this.enableScanCropRectOnly = enableScanCropRectOnly;
    this.formats = formats;
  }
```
|     Parameter    |   Description         | 
| ------------- |:-------------:| 
| enableVibration      | vibrate your phone when a barcode is detected |
| enableBeep      |   play a beep sound when a barcode is detected    |  
| enableAutoZoom |   the library will zoom in/out automatcially to scan a barcode    |   
| enableScanCropRectOnly |   only scan the view finder area    |   
| formats |   the barcode formats    |  
