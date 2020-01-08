---
title: "\"/\" オブジェクト (/)"
description: 必要なのは、クライアントのスキャン要求に対する WSD Scan サービスの応答です。
ms.assetid: a832bdc2-9c47-41da-ac78-a844b8f84ec1
keywords:
- オブジェクトのイメージ作成デバイス
topic_type:
- apiref
api_name:
- wscn CreateScanJobResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa2db14d95976c4f47c68b53cf5f60ea6593648
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652986"
---
# <a name="createscanjobresponse-element"></a>"/" オブジェクト (/)


必要なのは、クライアントのスキャン要求に対する WSD Scan サービスの**応答です。**

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

WSD スキャンサービスで**は、"/" をサポート**する必要があります。

WSD Scan サービスは、クライアントの[**メッセージの出力**](createscanjobrequest.md)に応答して、クライアントに対して、**出力操作要素を送信**します。

クライアントが有効なスキャン要求を行った場合、WSD Scan サービスは次の情報を返す必要があります。

-   ジョブを識別する一意の[**JobId**](jobid.md) 。 スキャナーは、定義された範囲内で、実装によって定義された方法で**JobId**を生成します。 スキャンサービスでは、クライアントがジョブを古いジョブと混同しないように、最近割り当てられた値を再利用することはできません。
-   JobToken 内の一意の識別子。 JobToken は、スキャンジョブを一意に表すために JobId とペアになっています。 JobToken は RetrieveImageRequest operation 要素の Scan サービスに渡されます。これにより、スキャンデバイスはスキャンの依頼者がスキャンジョブを実際に作成したことを確認できます。
-   ImageInformation。この情報には、現在検証中の ScanTicket を使用して行われたスキャンの結果のイメージデータに関する情報が含まれています。
-   DocumentFinalParameters。スキャンサービスがこのスキャンジョブに使用する実際の DocumentParameters 要素が含まれています。

クライアントは、1つまたは複数の[**RetrieveImageRequest**](retrieveimagerequest.md) operation 要素を送信することによって、スキャンサービスから実際のイメージデータを取得する必要があります。 クライアントの RetrieveImageRequest operation 要素を送信するには、クライアントの operation[**要求**](createscanjobrequest.md)に対してスキャンサービスが応答した後、60秒かかります。 この時間内にスキャンサービスが**RetrieveImageRequest**を受信しない場合は、 [**JobStateReason**](jobstatereason.md)の**JobTimedOut**を使用してジョブを中止する必要があります。 ジョブが複数のドキュメントで構成されている場合、このタイムアウトは、連続する**RetrieveImageRequest/Response**操作の間に適用されます。

<a name="examples"></a>例
--------

次のコード例では、"/" を使用して、この要求に対する WSD Scan サービスの応答を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
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

## <a name="see-also"></a>「


[ **//ジョブ要求**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**ImageInformation**](imageinformation.md)

[**JobId**](jobid.md)

[**JobStateReason**](jobstatereason.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






