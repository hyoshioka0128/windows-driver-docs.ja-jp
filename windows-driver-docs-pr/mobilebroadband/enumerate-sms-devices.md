---
title: SMS デバイスの列挙
description: SMS デバイスの列挙
ms.assetid: d0d57a4f-df83-4f3b-b7b4-417ad4e11350
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce34411624b6ee9b972b8d2160084463ba2b18d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381486"
---
# <a name="enumerate-sms-devices"></a>SMS デバイスの列挙


モバイル ブロード バンド SMS プラットフォームでは、最初 SMS 対応モバイル ブロード バンド デバイス、または、すべての SMS 対応モバイル ブロード バンド デバイスの一覧を取得する機能を提供します。 次のサンプル コードでは、既定の SMS デバイスと、特定のデバイスは、SMS オブジェクトをインスタンス化を示します。

**注**  を使用するアプリでC#または C++ で Windows 8、Windows 8.1、または Windows 10 での最初の使用、 [ **SmsDevice** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Sms.SmsDevice)を呼び出すオブジェクト[ **GetDefaultAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Sms.SmsDevice#Windows_Devices_Sms_SmsDevice_GetDefaultAsync)または[ **FromIdAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Sms.SmsDevice#Windows_Devices_Sms_SmsDevice_FromIdAsync_System_String_) STA スレッドでする必要があります。 MTA スレッドからの呼び出しと、未定義の動作があります。

 

**既定の SMS デバイスを使用する JavaScript コードの例**

``` syntax
var smsDevice = new Windows.Devices.Sms.SmsDevice.getDefault();

try
{
  var smsDeviceOperation = Windows.Devices.Sms.SmsDevice.getDefaultAsync();
  smsDeviceOperation.done(smsDeviceReceived, errorCallback);
}
catch (err)
{
  // handle error
}
```

**SMS のすべてのデバイスを列挙するために JavaScript コードの例**

``` syntax
Windows.Devices.Enumeration.DeviceInformation.findAllAsync(Windows.Devices.Sms.SmsDevice.getDeviceSelector()).then(function (smsdevices) 
{
  if (smsdevices.length > 0)
  {
    // for simplicity we choose the first device
    var smsDeviceId = smsdevices[0].Id;
    var smsDeviceOperation = Windows.Devices.Sms.SmsDevice.fromIdAsync(smsNotificationDetails.deviceId); 
    smsDeviceOperation.done(function (smsDeviceResult)
    {
      smsDevice = smsDeviceResult;
    }, errorCallback);
  }
}
```

## <a name="span-iddetecterrspanspan-iddetecterrspandetect-sms-device-access-errors"></a><span id="detecterr"></span><span id="DETECTERR"></span>SMS デバイスへのアクセス エラーを検出します。


SMS を列挙するデバイスが失敗したかどうか、アプリに SMS へのアクセスがあるないためにを検出できます。 これは、ユーザーが明示的に、アプリへのアクセスを拒否した場合、またはデバイスのメタデータは、アプリへのアクセスを付与していない場合に発生することができます。

**SMS デバイスへのアクセス エラーを検出する JavaScript コードの例**

``` syntax
Windows.Devices.Enumeration.DeviceInformation.findAllAsync(Windows.Devices.Sms.SmsDevice.getDeviceSelector()).then(function (smsdevices)
{
  if (smsdevices.length > 0)
  {
    // for simplicity we choose the first device
    var smsDeviceId = smsdevices[0].Id.slice(startIndex,endIndex + 1);
    var smsDeviceOperation = Windows.Devices.Sms.SmsDevice.fromIdAsync(smsNotificationDetails.deviceId); 
    smsDeviceOperation.done(function (smsDeviceResult)
    {
      smsDevice = smsDeviceResult;
    }, errorCallback); 

    // detect if SMS access is denied due to user not granting app consent to use SMS or if metadata is missing or invalid.

  }

function errorCallback(error)
{
  WinJS.log(error.name + " : " + error.description, "sample", "error");

  // If the error was caused due to access being denied to this app
  // then the HResult is set to E_ACCESSDENIED (0x80007005)

  // var hResult = hex(error.number);

}

function hex(nmb)
{
  if (nmb >= 0)
  {
    return nmb.toString(16);
  }
  else
  {
    return (nmb + 0x100000000).toString(16);
  }
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SMS のアプリの開発](developing-sms-apps.md)

 

 






