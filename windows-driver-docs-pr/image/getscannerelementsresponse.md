---
title: GetScannerElementsResponse 要素
description: 必要な GetScannerElementsResponse 要素には、クライアントの要求については、スキャナーに WSD スキャン サービスの応答が含まれています。
ms.assetid: da3cded6-6aa9-4fe6-ad02-9a02d2219075
keywords:
- GetScannerElementsResponse 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn GetScannerElementsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea5031172bf4368c685659885bd74c64a156b2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535755"
---
# <a name="getscannerelementsresponse-element"></a>GetScannerElementsResponse 要素


必要な**GetScannerElementsResponse**要素にはについて、スキャナーは、クライアントの要求への WSD スキャン サービスの応答が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:GetScannerElementsResponse>
  child elements
</wscn:GetScannerElementsResponse>
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
<td><p><a href="scannerelements.md" data-raw-source="[&lt;strong&gt;ScannerElements&lt;/strong&gt;](scannerelements.md)"><strong>ScannerElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスをサポートする必要があります、 **GetScannerElementsResponse**操作の要素。

ときにクライアントが正常にスキャナーを使用して情報を照会、 [ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作で、スキャン サービスが応答する必要があります、 **GetScannerElementsResponse**要求された情報が含まれる要素を操作します。

<a name="examples"></a>例
--------

次のコード例では、WSD スキャン サービスは、スキャナーの説明を返します。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetScannerElementsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsResponse>
      <wscn:ScannerElements>
        <wscn:ElementData wscn:Name="wscn:ScannerDescription" wscn:Valid="true">
        <wscn:ScannerDescription>
          <wscn:ScannerName xml:lang="en-AU, en-CA, en-GB, en-US" >
            Accounting Scanner in Copy Room 2
          </wscn:ScannerName >
          <wscn:ScannerInfo xml:lang="en-AU, en-CA, en-GB, en-US" >
            Scanner for use of Accounting only
          </wscn:ScannerInfo >
          <wscn:ScannerLocation xml:lang="en-AU, en-CA, en-GB, en-US" >
            LA Campus - Building 3
          </wscn:ScannerLocation >
        </wscn:ScannerDescription>
        </wscn:ElementData>
      </wscn:ScannerElements>
    </wscn:GetScannerElementsResponse>
  </soap:Body>
</soap:Envelope>
```

次のコード例では、スキャナーの状態要求に対する応答を示しています。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetScannerElementsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsResponse>
      <wscn:ScannerElements>
        <wscn:ElementData wscn:Name="wscn:ScannerStatus" wscn:Valid="true">
          <wscn:ScannerStatus>
            <wscn:ScannerCurrentTime>
              2006-01-26T11:17:00Z
            </wscn:ScannerCurrentTime>
            <wscn:ScannerState>Stopped</wscn:ScannerState>
            <wscn:ScannerStateReasons>
              <wscn:ScannerStateReason>MediaJam</wscn:ScannerStateReason>
              <wscn:ScannerStateReason>LampError</wscn:ScannerStateReason>
            </wscn:ScannerStateReasons>
            <wscn:ActiveConditions>
              <wscn:DeviceCondition wscn:Id="1384">
                <wscn:Time>2005-01-26T11:07:00Z</wscn:Time>
                <wscn:Name>MediaJam</wscn:Name>
                <wscn:Component>MediaPath</wscn:Component>
                <wscn:Severity>Critical</wscn:Severity>
              </wscn:DeviceCondition>
              <wscn:DeviceCondition wscn:Id="534">
                <wscn:Time>2005-01-26T11:09:12Z</wscn:Time>
                <wscn:Name>LampError</wscn:Name>
                <wscn:Component>Platen</wscn:Component>
                <wscn:Severity>Warning</wscn:Severity>
              </wscn:DeviceCondition>
            </wscn:ActiveConditions>
          </wscn:ScannerStatus>
        </wscn:ElementData>
      </wscn:ScannerElements>
    </wscn:GetScannerElementsResponse>
  </soap:Body>
</soap:Envelope>
```

次のコード例は、両方を含む GetScannerElementsRequest 操作に対する応答を示しています。 スキャナー構成要求とエントリが無効です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  xmlns:ihv="http://www.example.com/extension"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetScannerElementsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsResponse>
      <wscn:ScannerElements>
        <wscn:ElementData wscn:Name="wscn:ScannerConfiguration"
                          wscn:Valid="true">
          <wscn:ScannerConfiguration>
            <wscn:DeviceSettings>
              <wscn:FormatsSupported>
                <wscn:FormatValue>dib</wscn:FormatValue>
                <wscn:FormatValue>exif</wscn:FormatValue>
                <wscn:FormatValue>jpeg2k</wscn:FormatValue>
                <wscn:FormatValue>pdf-a</wscn:FormatValue>
                <wscn:FormatValue>png</wscn:FormatValue>
                <wscn:FormatValue>tiff-single-uncompressed</wscn:FormatValue>
                <wscn:FormatValue>tiff-single-g4</wscn:FormatValue>
                <wscn:FormatValue>tiff-multi-uncompressed</wscn:FormatValue>
                <wscn:FormatValue>tiff-multi-g4</wscn:FormatValue>
                <wscn:FormatValue>xps</wscn:FormatValue>
              </wscn:FormatsSupported>
              <wscn:CompressionQualityFactorSupported>
                <wscn:MinValue>15</wscn:MinValue>
                <wscn:MaxValue>100</wscn:MaxValue>
              </wscn:CompressionQualityFactorSupported>
              <wscn:ContentTypesSupported>
                <wscn:ContentTypeValue>Auto</wscn:ContentTypeValue>
                <wscn:ContentTypeValue>Text</wscn:ContentTypeValue>
                <wscn:ContentTypeValue>Photo</wscn:ContentTypeValue>
                <wscn:ContentTypeValue>Halftone</wscn:ContentTypeValue>
                <wscn:ContentTypeValue>Mixed</wscn:ContentTypeValue>
              </wscn:ContentTypesSupported>
              <wscn:DocumentSizeAutoDetectSupported>
                true
              </wscn:DocumentSizeAutoDetectSupported>
              <wscn:AutoExposureSupported>true</wscn:AutoExposureSupported>
              <wscn:BrightnessSupported>true</wscn:BrightnessSupported>
              <wscn:ContrastSupported>true</wscn:ContrastSupported>
              <wscn:ScalingRangeSupported>
                <wscn:ScalingWidth>
                  <wscn:MinValue>50</wscn:MinValue>
                  <wscn:MaxValue>500</wscn:MaxValue>
                </wscn:ScalingWidth>
                <wscn:ScalingHeight>
                  <wscn:MinValue>50</wscn:MinValue>
                  <wscn:MaxValue>500</wscn:MaxValue>
                </wscn:ScalingHeight>
              </wscn:ScalingRangeSupported>
              <wscn:RotationsSupported>
                <wscn:RotationValue>0</wscn:RotationValue>
                <wscn:RotationValue>90</wscn:RotationValue>
                <wscn:RotationValue>180</wscn:RotationValue>
                <wscn:RotationValue>270</wscn:RotationValue>
              </wscn:RotationsSupported>
            </wscn:DeviceSettings>

            <wscn:Platen>
              <wscn:PlatenOpticalResolution>
                <wscn:Width>1200</wscn:Width>
                <wscn:Height>1200</wscn:Height>
              </wscn:PlatenOpticalResolution>
              <wscn:PlatenResolutions>
                <wscn:Widths>
                  <wscn:Width>150</wscn:Width>
                  <wscn:Width>204</wscn:Width>
                  <wscn:Width>300</wscn:Width>
                  <wscn:Width>600</wscn:Width>
                  <wscn:Width>1200</wscn:Width>
                </wscn:Widths>
                <wscn:Heights>
                  <wscn:Height>96</wscn:Height>
                  <wscn:Height>150</wscn:Height>
                  <wscn:Height>204</wscn:Height>
                  <wscn:Height>300</wscn:Height>
                  <wscn:Height>600</wscn:Height>
                  <wscn:Height>900</wscn:Height>
                  <wscn:Height>1200</wscn:Height>
                </wscn:Heights>
              </wscn:PlatenResolutions>
              <wscn:PlatenColor>
                <wscn:ColorEntry>BlackAndWhite1</wscn:ColorEntry>
                <wscn:ColorEntry>Grayscale4</wscn:ColorEntry>
                <wscn:ColorEntry>Grayscale8</wscn:ColorEntry>
                <wscn:ColorEntry>RGB24</wscn:ColorEntry>
                <wscn:ColorEntry>RGB48</wscn:ColorEntry>
                <wscn:ColorEntry>RGBa32</wscn:ColorEntry>
                <wscn:ColorEntry>RGBa64</wscn:ColorEntry>
              </wscn:PlatenColor>
              <wscn:PlatenMinimumSize>
                <wscn:Width>250</wscn:Width>
                <wscn:Height>250</wscn:Height>
              </wscn:PlatenMinimumSize>
              <wscn:PlatenMaximumSize>
                <wscn:Width>11000</wscn:Width>
                <wscn:Height>14000</wscn:Height>
              </wscn:PlatenMaximumSize>
            </wscn:Platen>

            <wscn:ADF>
              <wscn:ADFSupportsDuplex>false</wscn:ADFSupportsDuplex>
              <wscn:ADFFront>
                <wscn:ADFOpticalResolution>
                  <wscn:Width>600</wscn:Width>
                  <wscn:Height>600</wscn:Height>
                </wscn:ADFOpticalResolution>
                <wscn:ADFResolutions>
                  <wscn:Widths>
                    <wscn:Width>150</wscn:Width>
                    <wscn:Width>204</wscn:Width>
                    <wscn:Width>300</wscn:Width>
                    <wscn:Width>600</wscn:Width>
                  </wscn:Widths>
                  <wscn:Heights>
                    <wscn:Height>96</wscn:Height>
                    <wscn:Height>150</wscn:Height>
                    <wscn:Height>204</wscn:Height>
                    <wscn:Height>300</wscn:Height>
                    <wscn:Height>600</wscn:Height>
                  </wscn:Heights>
                </wscn:ADFResolutions>
                <wscn:ADFColor>
                  <wscn:ColorEntry>BlackAndWhite1</wscn:ColorEntry>
                  <wscn:ColorEntry>Grayscale4</wscn:ColorEntry>
                  <wscn:ColorEntry>RGB24</wscn:ColorEntry>
                </wscn:ADFColor>
                <wscn:ADFMinimumSize>
                  <wscn:Width>4000</wscn:Width>
                  <wscn:Height>6000</wscn:Height>
                </wscn:ADFMinimumSize>
                <wscn:ADFMaximumSize>
                  <wscn:Width>8500</wscn:Width>
                  <wscn:Height>11000</wscn:Height>
                </wscn:ADFMaximumSize>
              </wscn:ADFFront>
            </wscn:ADF>

            <wscn:Film>
              <wscn:FilmScanModesSupported>
                <wscn:FilmScanModeValue>
                  ColorSlideFilm
                </wscn:FilmScanModeValue>
                <wscn:FilmScanModeValue>
                  ColorNegativeFilm
                </wscn:FilmScanModeValue>
                <wscn:FilmScanModeValue>
                  BlackandWhiteNegativeFilm
                </wscn:FilmScanModeValue>
              </wscn:FilmScanModesSupported>
              <wscn:FilmOpticalResolution>
                <wscn:Width>600</wscn:Width>
                <wscn:Height>600</wscn:Height>
              </wscn:FilmOpticalResolution>
              <wscn:FilmResolutions>
                <wscn:Widths>
                  <wscn:Width>150</wscn:Width>
                  <wscn:Width>300</wscn:Width>
                  <wscn:Width>600</wscn:Width>
                </wscn:Widths>
                <wscn:Heights>
                  <wscn:Height>150</wscn:Height>
                  <wscn:Height>300</wscn:Height>
                  <wscn:Height>600</wscn:Height>
                </wscn:Heights>
              </wscn:FilmResolutions>
              <wscn:FilmColor>
                <wscn:ColorEntry>BlackAndWhite1</wscn:ColorEntry>
                <wscn:ColorEntry>Grayscale4</wscn:ColorEntry>
                <wscn:ColorEntry>RGB24</wscn:ColorEntry>
                <wscn:ColorEntry>RGBa32</wscn:ColorEntry>
              </wscn:FilmColor>
              <wscn:FilmMinimumSize>
                <wscn:Width>1378</wscn:Width>
                <wscn:Height>1378</wscn:Height>
              </wscn:FilmMinimumSize>
              <wscn:FilmMaximumSize>
                <wscn:Width>2756</wscn:Width>
                <wscn:Height>10000</wscn:Height>
              </wscn:FilmMaximumSize>
            </wscn:Film>
          </wscn:ScannerConfiguration>
        </wscn:ElementData>
        <wscn:ElementData wscn:Name="ihv:InvalidRequestEntry"
                          wscn:Valid="false"/>
      </wscn:ScannerElements>
    </wscn:GetScannerElementsResponse>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>関連項目


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerElements**](scannerelements.md)

 

 






