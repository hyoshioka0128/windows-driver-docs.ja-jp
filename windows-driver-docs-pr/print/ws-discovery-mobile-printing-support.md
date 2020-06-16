---
title: WS-Discovery モバイル印刷サポート
description: WS-Discovery モバイル印刷サポート
ms.assetid: 788E2A1C-FBE9-40CD-A3EB-14A2DE266A2C
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: b053377542cba980c97f3cbb41ff9ec1838466b8
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793744"
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

| 定数/値 | 説明 |
|--|--|
| PNPX_DEVICECATEGORY_PRINTER_MOBILE<br><br>L "MobilePrinter" | MobilePrinter カテゴリ<br><br>キーワード: Printer |

デバイスカテゴリを WS-ADDRESSING メタデータ交換に追加する方法の詳細については、「 [pnp-x の仕様](https://docs.microsoft.com/previous-versions/gg463082(v=msdn.10))」を参照してください。
