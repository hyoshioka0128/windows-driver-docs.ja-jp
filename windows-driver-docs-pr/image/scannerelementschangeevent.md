---
title: Scanの要素の Changeevent 要素
description: 必須の Scanの Changeevent 要素は、スキャナーで変更が発生したことをクライアントに通知します。
ms.assetid: 5a3eb934-631d-432b-befa-c67360fe68d1
keywords:
- Scanの要素の Changeevent 要素のイメージングデバイス
topic_type:
- apiref
api_name:
- wscn ScannerElementsChangeEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10d89a5b510c6204bbad13fefb1b12b674a6d9b2
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653008"
---
# <a name="scannerelementschangeevent-element"></a>Scanの要素の Changeevent 要素


必須の**Scanの Changeevent**要素は、スキャナーで変更が発生したことをクライアントに通知します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerElementsChangeEvent>
  child elements
</wscn:ScannerElementsChangeEvent>
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
<td><p><a href="elementchanges.md" data-raw-source="[&lt;strong&gt;ElementChanges&lt;/strong&gt;](elementchanges.md)"><strong>ElementChanges</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャンサービスは、スキャナーで scanの[**description**](scannerdescription.md)、 [**scanの configuration**](scannerconfiguration.md)、 [**defaultscanticket**](defaultscanticket.md)、またはベンダーの拡張機能内で要素が変更された場合に、クライアントに**scanによって changeevent**要素を送信する必要があります。

**Scan? Elementelementchangeevent**の本体には、更新された要素の完全な XML を含む[**elementchanges**](elementchanges.md)要素が含まれている必要があります。 返された XML にオプションの要素がない場合、WSD Scan サービスは、サービスがその要素をサポートしなくなったことをクライアントに示します。 このサポートの変更は、フィルムスキャンオプションや二重スキャンモードなどのオプションを削除することによって発生する可能性があります。 クライアントは、変更された値を特定し、その内部データストアを更新する必要があることを判断するために、[以前のデータとの**Elementchanges** ] の情報を比較する必要があります。

<a name="examples"></a>例
--------

次のコード例は、フィルムスキャンオプションのインストールにより、デバイスが更新されたスキャナーの構成情報を報告する方法を示しています。

```xml
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScannerElementsChangeEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScannerElementsChangeEvent>
      <wscn:ElementChanges>
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
      </wscn:ElementChanges>
    </wscn:ScannerElementsChangeEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>「


[**DefaultScanTicket**](defaultscanticket.md)

[**ElementChanges**](elementchanges.md)

[**スキャンの構成**](scannerconfiguration.md)

[**スキャンの説明**](scannerdescription.md)

 

 






