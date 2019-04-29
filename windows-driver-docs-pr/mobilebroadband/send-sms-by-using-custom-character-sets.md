---
title: カスタム文字セットを使用して SMS を送信する
description: カスタム文字セットを使用して SMS を送信する
ms.assetid: c1f19c16-66f5-4bcd-ba28-950eaa6472d2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76d978497c3245c4168e9c20263f7c43fed6e6bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384648"
---
# <a name="send-sms-by-using-custom-character-sets"></a>カスタム文字セットを使用して SMS を送信する


テキスト モードのインターフェイスで生のメッセージ プロトコル データ ユニット (PDU) がサポートされていないシナリオを実現するためにへのアクセスを必要がある場合、Windows 8、Windows 8.1、および Windows 10 を有効にする PDU モード送信と受信 SMS メッセージを読み取るします。

次の場合に、PDU モード SMS インターフェイスを使用する必要があります。

-   送信や受信 SMS で定義されている言語 1 つの国内の shift キーをテーブルまたは各国語の言語ロック Shift テーブルを使用して読み取りに[3 gpp TS 23.038](https://go.microsoft.com/fwlink/?LinkId=329080)します。

-   マルチパートの SMS を送信するには、別の文字を使用して、セグメントごとに設定します。

**PDU モード インターフェイスを使用して SMS メッセージを送信する JavaScript コードの例**

``` syntax
function smsDevicePDUSend()
{
  if (smsDevice !== null)
  {
    // Defines a binary message
    var smsMessage = new Windows.Devices.Sms.SmsBinaryMessage();
    var messsagePdu = “0011000B914152828377F90000AA0CC8F71D14969741F977FD07”;
    var messagePduByteArray = hexToByteArray(messsagePdu);
    smsMessage.setData(messagePduByteArray);

    if (smsDevice.cellularClass === Windows.Devices.Sms.CellularClass.gsm)
    {
      smsMessage.format = Windows.Devices.Sms.SmsDataFormat.gsmSubmit;
    }
    else
    {
      smsMessage.format = Windows.Devices.Sms.SmsDataFormat.cdmaSubmit;
    }
    var sendSmsMessageOperation = smsDevice.sendMessageAsync(smsMessage);

    sendSmsMessageOperation.done(function (reply) {
      WinJS.log("Sent message in PDU format", "sample", "status");
    }, errorCallback);
}

// Used to convert hex PDU to byte array for sending SMS using PDU //mode
function hexToByteArray(hexString)
{
  var result = [];
  var hexByte = "";
  var decByte = 0;
  for (var i = 0; i < hexString.length; i = i + 2) {
    hexByte = hexString.substring(i, i + 2);
    decByte = parseInt(hexByte, 16);
    result.push(decByte);
  }
  return result;
}
```

**PDU モード インターフェイスを使用して受信 SMS メッセージを読み取るための JavaScript コードの例**

``` syntax
function smsDeviceRead()
{
  try
  {
    if (smsDevice !== null)
    {
      var messageStore = smsDevice.messageStore;
      var messageID = “1” // select a Message Id to read 

      // Check for a valid ID number
      if (isNaN(messageID) || messageID < 1 || messageID > messageStore.maxMessages)
      {
        WinJS.log("Invalid ID number", "sample", "error");
        return;
     }

     var getSmsMessageOperation = messageStore.getMessageAsync(messageID);

     // Display message when get is completed
     getSmsMessageOperation.done(smsMessageReadSuccess, errorCallback);
     } 
  }
  catch (err) {
    // handle error
  }
}

function smsMessageReadSuccess(smsMessage)
{
  try
  {
    if (smsMessage instanceof SmsBinaryMessage) {
    var format  = smsMessage.format;
    var pduData = smsMessage.getData(); // byte array 
  }
  catch (err)
  {
    WinJS.log("SMS did not set up: " + err, "sample", "error");
  }
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SMS のアプリの開発](developing-sms-apps.md)

 

 






