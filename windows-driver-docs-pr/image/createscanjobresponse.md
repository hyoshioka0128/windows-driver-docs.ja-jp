---
title: CreateScanJobResponse 要素
description: 必要な CreateScanJobResponse 要素には、クライアントのスキャン要求への WSD スキャン サービスの応答が含まれています。
ms.assetid: a832bdc2-9c47-41da-ac78-a844b8f84ec1
keywords:
- CreateScanJobResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn CreateScanJobResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd61b561afd387dc7cf0c9a6d16d01996a15beb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370974"
---
# <a name="createscanjobresponse-element"></a>CreateScanJobResponse 要素


必要な**CreateScanJobResponse**要素には、クライアントのスキャン要求への WSD スキャン サービスの応答が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:CreateScanJobResponse>
  child elements
</wscn:CreateScanJobResponse>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="imageinformation.md" data-raw-source="[&lt;strong&gt;ImageInformation&lt;/strong&gt;](imageinformation.md)"><strong>ImageInformation</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobtoken.md" data-raw-source="[&lt;strong&gt;JobToken&lt;/strong&gt;](jobtoken.md)"><strong>JobToken</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **CreateScanJobResponse**操作の要素。

WSD スキャン サービスに送信、 **CreateScanJobResponse**操作の要素をクライアントに応答をクライアントの[ **CreateScanJobRequest**](createscanjobrequest.md)します。

クライアントには、有効なスキャン要求が行われて、WSD スキャン サービスは、次の情報を返す必要があります。

-   一意[ **JobId** ](jobid.md)ジョブを識別します。 スキャナーが生成されます**JobId**定義した範囲内での実装定義のようにします。 スキャン サービスには、クライアントは、古いジョブのジョブを混同しないでくださいようにを最近割り当てられた値が再利用する必要があります。
-   JobToken の一意の識別子。 JobToken はスキャン ジョブを一意に表す JobId と組み合わせて使用します。 JobToken はスキャン要求元がスキャン ジョブを実際に作成されたことを確認するデバイスのスキャンを有効にする RetrieveImageRequest 操作の要素で、スキャン サービスに渡されます。
-   ImageInformation 現在検証されている ScanTicket によるスキャンから結果として得られるイメージ データに関する情報が含まれています。
-   DocumentFinalParameters スキャン サービスは、このスキャン ジョブに使用する実際の DocumentParameters 要素が含まれています。

クライアントは、実際の画像データを送信してスキャン サービスから 1 つまたは複数を取得する必要があります[ **RetrieveImageRequest** ](retrieveimagerequest.md)操作要素。 クライアントに送信する 60 秒、 **RetrieveImageRequest**操作の要素をクライアントのスキャン サービスが応答したら[ **CreateScanJobRequest**](createscanjobrequest.md)します。 スキャン サービスが受信しなかった場合、 **RetrieveImageRequest** 、この時間内にジョブを中止にする必要があります、 [ **JobStateReason** ](jobstatereason.md)の**JobTimedOut**. 場合は、ジョブは、複数のドキュメントで構成され、このタイムアウトが間に適用されます。 連続する各**RetrieveImageRequest/応答**操作。

<a name="examples"></a>例
--------

次のコード例では、WSD スキャン サービス応答を CreateScanJobRequest を示しています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheCreateScanJobRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:CreateScanJobResponse>
      <wscn:JobId>1</wscn:JobId>
      <wscn:JobToken>Job9876TokenString</wscn:JobToken>
      <wscn:ImageInformation>
        <wscn:MediaFrontImageInfo>
          <wscn:PixelsPerLine>900</wscn:PixelsPerLine>
          <wscn:NumberOfLines>1500</wscn:NumberOfLines>
          <wscn:BytesPerLine>113</wscn:BytesPerLine>
        </wscn:MediaFrontImageInfo>
      </wscn:ImageInformation>
      <wscn:DocumentFinalParamters>
        <wscn:Format>jfif</wscn:Format>
        <wscn:CompressionQualityFactor>45</wscn:CompressionQualityFactor>
        <wscn:ImagesToTransfer>0</wscn:ImagesToTransfer>
        <wscn:InputSource>Platen</wscn:InputSource>
        <wscn:ContentType>Auto</wscn:ContentType>
        <wscn:InputSize>
          <wscn:InputMediaSize>
            <wscn:Width wscn:Override="true">8500</wscn:Width>
            <wscn:Height wscn:Override="true">11000</wscn:Height>
          </wscn:InputMediaSize>
        </wscn:InputSize>
        <wscn:Exposure>
          <wscn:ExposureSettings>
            <wscn:Contrast wscn:UsedDefault="true">0</wscn:Contrast>
            <wscn:Brightness wscn:UsedDefault="true">0</wscn:Brightness>
            <wscn:Sharpness wscn:UsedDefault="true">0</wscn:Sharpness>
          </wscn:ExposureSettings>
        </wscn:Exposure>
        <wscn:Scaling>
          <wscn:ScalingWidth>125</wscn:ScalingWidth>
          <wscn:ScalingHeight>125</wscn:ScalingHeight>
        </wscn:Scaling>
        <wscn:Rotation wscn:UsedDefault="true">0</wscn:Rotation>
        <wscn:MediaSides>
          <wscn:MediaFront>
            <wscn:ScanRegion>
              <wscn:ScanRegionXOffset wscn:UsedDefault="true">
                0
              </wscn:ScanRegionXOffset>
              <wscn:ScanRegionYOffset wscn:UsedDefault="true">
                0
              </wscn:ScanRegionYOffset>
              <wscn:ScanRegionWidth wscn:UsedDefault="true">
                8500
              </wscn:ScanRegionWidth>
              <wscn:ScanRegionHeight wscn:UsedDefault="true">
                11000
              </wscn:ScanRegionHeight>
            </wscn:ScanRegion>
            <wscn:ColorProcessing wscn:UsedDefault="true">
              RGB24
            </wscn:ColorProcessing>
            <wscn:Resolution>
              <wscn:Width>300</wscn:Width>
              <wscn:Height>300</wscn:Height>
            </wscn:Resolution>
          </wscn:MediaFront>
        </wscn:MediaSides>
      </wscn:DocumentFinalParamters>
    </wscn:CreateScanJobResponse>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**ImageInformation**](imageinformation.md)

[**JobId**](jobid.md)

[**JobStateReason**](jobstatereason.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






