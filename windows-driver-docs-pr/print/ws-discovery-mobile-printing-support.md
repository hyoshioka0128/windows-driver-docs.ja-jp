---
title: WS-Discovery モバイル印刷サポート
description: WS-Discovery モバイル印刷サポート
ms.assetid: 788E2A1C-FBE9-40CD-A3EB-14A2DE266A2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36a8a8ccec4716ec84a40412553f42e88a12fafc
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652750"
---
# <a name="ws-discovery-mobile-printing-support"></a>WS-Discovery モバイル印刷サポート


Windows 10 Mobile からの印刷をサポートするデバイスでは、次の例に示すように、MobilePrinter カテゴリを WS-I Discovery モデルの応答に追加する必要があります。

```xml
<soap:Envelope
    xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wsdisco="https://schemas.xmlsoap.org/ws/2005/04/discovery"
    xmlns:wsx="https://schemas.xmlsoap.org/ws/2004/09/mex"
    xmlns:wsd="https://schemas.xmlsoap.org/ws/2006/02/devprof"
    xmlns:pnpx="https://schemas.microsoft.com/windows/pnpx/2005/10"> 

    <soap:Header>
        <!-- Place SOAP header information here.-->
    </soap:Header>   

    <soap:Body>
        <wsx:Metadata>
            <wsx:MetadataSection
                Dialect="https://schemas.xmlsoap.org/ws/2005/05/devprof/ThisDevice">
                <wsd:ThisDevice>
                    <!-- Place ThisDevice metadata here.-->
                </wsd:ThisDevice>
            </wsx:MetadataSection>
                
           <wsx:MetadataSection
                Dialect="https://schemas.xmlsoap.org/ws/2005/05/devprof/ThisModel">
                <wsd:ThisModel>
                    <!-- Place ThisModel metadata here.-->              
                    <pnpx:DeviceCategory>
                        <!-- This device is in the Printers category -->
                        Printers Scanners MobilePrinter
                   </pnpx:DeviceCategory>   
                </wsd:ThisModel>
            </wsx:MetadataSection>  

            <wsx:MetadataSection
                Dialect="https://schemas.xmlsoap.org/ws/2005/05/devprof/Relationship">
                <wsd:Relationship
                    Type="https://schemas.xmlsoap.org/ws/2005/05/devprof/host">

                    <wsd:Hosted>
                        <!-- Place Hosted metadata for the 
                             first service here.-->
                        <pnpx:HardwareId>
                            <!-- Place the Hardware ID for the first service here.-->
                            PnPX_SampleService1_HWID    
                        </pnpx:HardwareId>
                        <pnpx:CompatibleId>
                            <!-- Place the Compatible ID for the first service here.-->
                            PnPX_SampleService1_CPID    
                        </pnpx:CompatibleId>
                    </wsd:Hosted>
                                                
                </wsd:Relationship>
            </wsx:MetadataSection>

        </wsx:Metadata>
    </soap:Body>
</soap:Envelope>
```

次の表に、MobilePrinter category キーワードに関する追加情報を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>定数/値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PNPX_DEVICECATEGORY_PRINTER_MOBILE</p>
<p>L "MobilePrinter"</p></td>
<td><p>MobilePrinter カテゴリ</p>
<p>キーワード: Printer</p></td>
</tr>
</tbody>
</table>

 

デバイスカテゴリを WS-ADDRESSING メタデータ交換に追加する方法の詳細については、「 [pnp-x の仕様](https://go.microsoft.com/fwlink/p/?linkid=509797)」を参照してください。

 

 




