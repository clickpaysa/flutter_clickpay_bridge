# Flutter Clickpay Bridge
![Version](https://img.shields.io/badge/flutter%20clickpay%20bridge-v2.4.4-green)

Flutter ClickPay plugin is a wrapper for the native ClickPay Android and iOS SDKs, It helps you integrate with ClickPay payment gateway.

Plugin Support:

* [x] iOS
* [x] Android

# Installation

```
dependencies:
   flutter_clickpay_bridge: ^2.4.5
```

## Usage

```dart
import 'package:flutter_clickpay_bridge/*.dart';
```

### Pay with Card

1. Configure the billing & shipping info, the shipping info is optional

```dart
  var billingDetails = new BillingDetails("billing name", 
    "billing email", 
    "billing phone",
        "address line", 
        "country", 
        "city", 
        "state", 
        "zip code");
        
var shippingDetails = new ShippingDetails("shipping name", 
     "shipping email", 
     "shipping phone",
     "address line", 
     "country", 
     "city", 
     "state", 
     "zip code");
                                              
```

2. Create object of `PaymentSDKConfiguration` and fill it with your credentials and payment details.

```dart

 var configuration = PaymentSdkConfigurationDetails(
        profileId: "profile id",
        serverKey: "your server key",
        clientKey: "your client key",
        cartId: "cart id",
        cartDescription: "cart desc",
        merchantName: "merchant name",
        screentTitle: "Pay with Card",
        billingDetails: billingDetails,
        shippingDetails: shippingDetails,
        locale: PaymentSdkLocale.EN, //PaymentSdkLocale.AR or PaymentSdkLocale.DEFAULT 
        amount: "amount in double",
        currencyCode: "Currency code",
        merchantCountryCode: "2 chars iso country code");
```

Options to show billing and shipping info

```dart
	configuration.showBillingInfo = true;
	configuration.showShippingInfo = true;
```

3. Start payment by calling `startCardPayment` method and handle the transaction details 

```dart

FlutterPaymentSdkBridge.startCardPayment(configuration, (event) {
      setState(() {
        if (event["status"] == "success") {
          // Handle transaction details here.
          var transactionDetails = event["data"];
          print(transactionDetails);
        } else if (event["status"] == "error") {
          // Handle error here.
        } else if (event["status"] == "event") {
          // Handle events here.
        }
      });
    });
     
```
### Pay with token secured 3ds
Start payment by calling `start3DSecureTokenizedCardPayment` method and handle the transaction details

```dart

FlutterPaymentSdkBridge.start3DSecureTokenizedCardPayment(configuration,
PaymentSDKSavedCardInfo("4111 11## #### 1111", "visa"),
"Token", (event) {
      setState(() {
        if (event["status"] == "success") {
          // Handle transaction details here.
          var transactionDetails = event["data"];
          print(transactionDetails);
        } else if (event["status"] == "error") {
          // Handle error here.
        } else if (event["status"] == "event") {
          // Handle events here.
        }
      });
    });
     
```
### Pay with token 
Start payment by calling `startTokenizedCardPayment` method and handle the transaction details

```dart

FlutterPaymentSdkBridge.startTokenizedCardPayment(configuration, toke, transactionReference, (event) {
      setState(() {
        if (event["status"] == "success") {
          // Handle transaction details here.
          var transactionDetails = event["data"];
          print(transactionDetails);
        } else if (event["status"] == "error") {
          // Handle error here.
        } else if (event["status"] == "event") {
          // Handle events here.
        }
      });
    });
     
```

### Tokenization
To enable tokenisation please follow the below instructions.
```dart
 // to request token and transaction reference pass tokeniseType and Format
 tokeniseType: PaymentSdkTokeniseType.MERCHANT_MANDATORY,
 tokenFormat: PaymentSdkTokenFormat.AlphaNum20Format,

 // you will receive token and reference after the first transaction       
 // to pass the token and transaction reference returned from sdk 
 token: "token returned from the last trx",
 transactionReference: "last trx reference returned",

```
### Pay with Apple Pay

1. Follow the guide [Steps to configure Apple Pay][applepayguide] to learn how to configure ApplePay with ClickPay.

2. Do the steps 1 and 2 from **Pay with Card** although you can ignore Billing & Shipping details and Apple Pay will handle it, also you must pass the **merchant name** and **merchant identifier**.

```dart
//ignore this part if you want to use default networks
 List<PaymentSDKNetworks> networks = [];
    networks.add(PaymentSDKNetworks.visa);
    networks.add(PaymentSDKNetworks.amex);

 var configuration = PaymentSdkConfigurationDetails(
        profileId: "profile id",
        serverKey: "your server key",
        clientKey: "your client key",
        cartId: "cart id",
        cartDescription: "cart desc",
        merchantName: "merchant name",
        screentTitle: "Pay with Card",
        locale: PaymentSdkLocale.AR, //PaymentSdkLocale.EN or PaymentSdkLocale.DEFAULT 
        amount: "amount in double",
        currencyCode: "Currency code",
        merchantCountryCode: "2 chars iso country code",
        merchantApplePayIndentifier: "merchant.com.bundleID",
    paymentNetworks: networks);
```

3. To simplify ApplePay validation on all user's billing info, pass **simplifyApplePayValidation** parameter in the configuration with **true**.

```dart

configuration.simplifyApplePayValidation = true;

```

4. Call `startApplePayPayment` to start payment

```dart
FlutterPaymentSdkBridge.startApplePayPayment(configuration, (event) {
      setState(() {
        setState(() {
        if (event["status"] == "success") {
          // Handle transaction details here.
          var transactionDetails = event["data"];
          print(transactionDetails);
        } else if (event["status"] == "error") {
          // Handle error here.
        } else if (event["status"] == "event") {
          // Handle events here.
        }
      });
      });
    });
```

### Pay with Samsung Pay

Pass Samsung Pay token to the configuration and call `startSamsungPayPayment`

```dart
configuration.samsungToken = "{Json token returned from the samsung pay payment}"
```

### Pay with Alternative Payment Methods

It becomes easy to integrate with other payment methods in your region like STCPay, OmanNet, KNet, Valu, Fawry, UnionPay, and Meeza, to serve a large sector of customers.

Do the steps 1 and 2 from Pay with Card.

Choose one or more of the payment methods you want to support.
```dart
List<PaymentSdkAPms> apms= new List();
apms.add(PaymentSdkAPms.KNET_DEBIT);
configuration.alternativePaymentMethods = apms
```
Start payment by calling ```dart startAlternativePaymentMethod``` method and handle the transaction details
```dart
FlutterPaymentSdkBridge.startAlternativePaymentMethod(generateConfig(), (event) {
 setState(() {
        if (event["status"] == "success") {
          // Handle transaction details here.
          var transactionDetails = event["data"];
          print(transactionDetails);
        } else if (event["status"] == "error") {
          // Handle error here.
        } else if (event["status"] == "event") {
          // Handle events here.
        }
      });
    });
}

```

## Query transaction

You can check the status of a transaction

1- first create PaymentSDKQueryConfiguration
```dart
var queryConfig = PaymentSDKQueryConfiguration(
    "ServerKey",
    "ClientKey",
    "Country Iso 2",
    "Profile Id",
    "Transaction Reference"
);
```

2- Call QuerySdkActivity.queryTransaction and pass the needed arguments
```dart
FlutterPaytabsBridge.queryTransaction(
    queryConfig,
    (event) {
        setState(() {
            if (event["status"] == "success") {
                // Handle transaction details here.
                var transactionDetails = event["data"];
                print(transactionDetails);
            } else if (event["status"] == "error") {
                // Handle error here.
            } else if (event["status"] == "event") {
                // Handle events here.
            }
        });
    });
```

## Theme
### IOS
Use the following guide to cusomize the colors, font, and logo by configuring the theme and pass it to the payment configuration.

```dart
	var theme = IOSThemeConfigurations();
	theme.backgroundColor = "e0556e"; // Color hex value
	configuration.iOSThemeConfigurations = theme;
```

![UI guide](https://user-images.githubusercontent.com/103630680/179504994-db672cd2-0e1a-4467-a5fa-cab9c5e80e97.png)

### Android

## Override strings

To override string you can find the keys with the default values here
![english]( https://github.com/paytabscom/paytabs-android-library-sample/blob/master/res/strings.xml)
![arabic](https://github.com/paytabscom/paytabs-android-library-sample/blob/master/res/strings-ar.xml)

## Override colors
To override colors, make sure to you have colors.xml file inside Android resources or create one in the following path inside android folder: app/src/main/res/values/colors.xml

````xml

<resourse>
    // to override colors
    <color name="payment_sdk_primary_color">#5C13DF</color>
    <color name="payment_sdk_secondary_color">#FFC107</color>
    <color name="payment_sdk_primary_font_color">#111112</color>
    <color name="payment_sdk_secondary_font_color">#6D6C70</color>
    <color name="payment_sdk_separators_color">#FFC107</color>
    <color name="payment_sdk_stroke_color">#673AB7</color>
    <color name="payment_sdk_button_text_color">#FFF</color>
    <color name="payment_sdk_title_text_color">#FFF</color>
    <color name="payment_sdk_button_background_color">#3F51B5</color>
    <color name="payment_sdk_background_color">#F9FAFD</color>
    <color name="payment_sdk_card_background_color">#F9FAFD</color>

    // to override dimens
    <dimen name="payment_sdk_primary_font_size">17sp</dimen>
    <dimen name="payment_sdk_secondary_font_size">15sp</dimen>
    <dimen name="payment_sdk_separator_thickness">1dp</dimen>
    <dimen name="payment_sdk_stroke_thickness">.5dp</dimen>
    <dimen name="payment_sdk_input_corner_radius">8dp</dimen>
    <dimen name="payment_sdk_button_corner_radius">8dp</dimen>

</resourse>
````

## Enums

Those enums will help you in customizing your configuration.

* Tokenise types

 The default type is none

```dart
enum PaymentSdkTokeniseType {
  NONE,
  USER_OPTIONAL,
  USER_MANDATORY,
  MERCHANT_MANDATORY
}

```

```dart
configuration.tokeniseType = PaymentSdkTokeniseType.USER_OPTIONAL;
```

* Token formats

The default format is hex32

```dart
enum PaymentSdkTokenFormat {
  Hex32Format,
  NoneFormat,
  AlphaNum20Format,
  Digit22Format,
  Digit16Format,
  AlphaNum32Format
}
```

```javascript
configuration.tokenFormat = PaymentSdkTokenFormat.Hex32Format
```
## Demo application

Check our complete example here <https://github.com/clickpaysa/flutter_clickpay_bridge/tree/main/example>.

<img src="https://user-images.githubusercontent.com/103630680/179504080-e7dee58c-a879-4aa8-b6f4-e2951be63d70.png" />

## ClickPay

[Support][1]

 [1]: https://support.clickpay.com.sa/en/support/home
 [applepayguide]: https://github.com/clickpaysa/flutter_clickpay_bridge/blob/main/ApplePayConfiguration.md
