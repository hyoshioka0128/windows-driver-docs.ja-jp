---
title: Web Services on Devices (Ws-print) を印刷します。
description: 印刷およびスキャンの周辺機器を接続プロトコルを提供する、Windows Vista で導入された印刷 (Print WS) のデバイス上のサービスを web です。
ms.assetid: 4A641EF8-FBD3-46CA-9284-28AF1A4B8226
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c4afbe76e0f522c62d3785d7b416680503e10b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553778"
---
# <a name="web-services-on-devices-for-printing-ws-print"></a>Web Services on Devices (Ws-print) を印刷します。


印刷およびスキャンの周辺機器を接続プロトコルを提供する、Windows Vista で導入された印刷 (Print WS) のデバイス上のサービスを web です。

## <a name="overview"></a>概要


Web サービス テクノロジには、記述すると、情報を共有する共通のフレームワークが提供されます。 その結果、Windows が付属、一連のプロトコルを使用し、ネットワークに接続されたデバイス上のサービスを制御します。

印刷およびスキャン、デバイスの製造元を接続する、インストール、および Windows のデバイスを使用して強化されたカスタマー エクスペリエンスを活用する 4 つの Web サービス仕様が存在します。

## <a name="ws-print-v11"></a>Ws-print v1.1


Windows 8 では、services on devices (WSD) の web の印刷スキーマは、v1.1 に更新されました。 このバージョンのスキーマ (Ws-print v1.1 と呼ばれます) は、拡張ドライバー構成をサポートしてより色のインクまたはトナーとデバイスの表現のモデル Id に更新されました。

## <a name="ws-print-v12"></a>WS 印刷 v1.2


Windows 8.1 では、WS 印刷には、すべての操作と Ws-print v1.1 で使用されるスキーマの要素が含まれていますが、デバイス上の web サービスの印刷サービス定義が更新されました。 印刷用のデバイスでの結果として得られる新しい Web サービスは Ws-print v1.2 です。

新しいスキーマの WS 印刷バージョン 1.2 のサポートでは、要素と、新しい操作が追加されました。 新しいスキーマ要素"SupportsWSPrintV12"は、WS 印刷バージョン 1.2 のサポートを識別するために使用されます。 新しい操作では、"SetPrinterElements"により、クライアント プリンターのスキーマ要素の値を設定できます。 など、クライアントは、インク ジェット ヘッドを再配置するプリンターを使用する"InkHeadAlignmentValue"と呼ばれるカスタム要素を設定する可能性があります。

便宜上、仕様は、ここでは、それに関連付けられたと共に、スタンドアロンの完全な形式でダウンロード セクションで Web サービス記述言語 (Wsdl) と XML スキーマ定義 (Xsd)。 これら 4 つの Web サービスのデバイスの仕様には、Windows ドライバー開発キット (WDK) を参照する技術ドキュメントが含まれる使用許諾契約が適用されます。

次のセクションでは、WS 印刷のさまざまな側面に関するより詳細な情報を提供します。

## <a name="sequence-diagrams"></a>シーケンス図


次のシーケンス図は、サポートされている WS 印刷名前空間のバージョンを判断するためにクライアントとプリンターの間の相互作用を示していて、拡張スキーマの要素を取得します。

**Ws-print v1.1**します。 Ws-print v1.1 をサポートしているプリンターの相互作用のシーケンス図を次に示します。

![シーケンス図は、ws 印刷 v1.1 サポートに関する相互作用とプリンターの説明と構成の後続のクエリは、クライアント プリンターを表示します。](images/wsprint-diagv11.png)

プリンターをサポートする Ws-print v1.1、クライアントから GetPrinterElements(wprt:PrinterDescription) クエリに応答プリンター送信がされていることを示す情報。

Ws-print v1.1 をサポートしていること確認すると、プリンター後、は、クライアントが GetPrinterElements(wprt11:DriverConfiguration) クエリを送信し、プリンターが要求されたドライバーの構成情報で応答します。

**WS 印刷 v1.2**します。 WS 印刷バージョン 1.2 をサポートしているプリンターの相互作用のシーケンス図を次に示します。

![シーケンス図は、ws 印刷バージョン 1.2 のサポートに関する相互作用とプリンターの説明と構成の後続のクエリは、クライアント プリンターを表示します。](images/wsprint-diagv12.png)

プリンターでは、WS 印刷バージョン 1.2 をサポートする場合、GetPrinterElements(wprt:PrinterDescription) クエリに、クライアントからの応答でプリンター情報を送信バックがされていることを示します。

さらに、プリンターは GetPrinterElements(wprt:PrinterDescription) 呼び出しに対する応答で wprt12:SupportsWSPrintV12 を返す必要があります。 その後、クライアントは、WS 印刷デバイスでサポートされているスキーマの 1 つまたは複数のデータ要素を設定する SetPrinterElements 操作を呼び出すことができます。

Ws-print v1.2 をサポートしていること確認すると、プリンター後、は、クライアントが GetPrinterElements(wprt12:DriverConfiguration) クエリを送信し、プリンターが要求されたドライバーの構成情報で応答します。

## <a name="namespaces"></a>名前空間


**Ws-print v1.1**

**Namespace:**<http://schemas.microsoft.com/windows/2010/06/wdp/printv11>
**XML の Namespace 定義:** xmlns:wprt12 ="<http://schemas.microsoft.com/windows/2012/10/wdp/printV12>"

**WS 印刷 v1.2**

**Namespace:**<http://schemas.microsoft.com/windows/2012/10/wdp/printV12>
**XML の Namespace 定義:** xmlns:wprt11 ="<http://schemas.microsoft.com/windows/2010/06/wdp/printv11>"
## <a name="specifying-ws-print-11-support"></a>WS 印刷 1.1 のサポートを指定します。


Ws-print 1.1 要素をサポートするプリンターは、その PrinterDescription wprt11:SupportsWSPrintv11 を含めるを更新する必要があります。 Wprt11:SupportsWSPrintv11 でない場合は true に設定して指定し、WSDMon は要求しません Ws-print 1.1 要素プリンターから。

Ws-print v1.1 をサポートしている印刷デバイスは、Windows の名前空間内の他の要素をクエリするためには、その PrinterDescription で次の内容を含める必要があります。

```xml
<soap:Envelope
...
  xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
...
  <wprt11:SupportsWSPrintv11>true</wprt11:SupportsWSPrintv11>
...
```

次の XML スニペットは、WSD 印刷サービス仕様 v1.0 から派生し、前のセクションで、コンテンツの適切な使用方法を示します。

```xml
<soap:Envelope
        xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
        xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
        xmlns:wprt="http://schemas.microsoft.com/windows/2006/08/wdp/print"
        xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
  <soap:Header>
    <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/08/wdp/print/GetPrinterElementsResponse
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetPrinterElementsRequest</wsa:RelatesTo>
  </soap:Header>
  <soap:Body>
    <wprt:GetPrinterElementsResponse>
      <wprt:PrinterElements>
        <wprt:ElementData Name="wprt:PrinterDescription" Valid="true">
          <wprt:PrinterDescription>
            <wprt:ColorSupported>true</wprt:ColorSupported>
            <wprt:DeviceId>MFG:Acme;MDL:PrintMaster 9020</wprt:DeviceId>
            <wprt:MultipleDocumentJobsSupported>true</wprt:MultipleDocumentJobsSupported>
            <wprt:PagesPerMinute>20</wprt:PagesPerMinute>
            <wprt:PagesPerMinuteColor>8</wprt:PagesPerMinuteColor>
            <wprt:PrinterName xml:lang="en-AU, en-CA, en-GB, en-US">
              Accounting Printer in Copy Room 2
            </wprt:PrinterName>
            <wprt:PrinterInfo xml:lang="en-AU, en-CA, en-GB, en-US">
              Printer for use of Accounting only
            </wprt:PrinterInfo>
            <wprt:PrinterLocation xml:lang="en-AU, en-CA, en-GB, en-US">
              LA Campus – Building 3
            </wprt:PrinterLocation>
            <wprt11:SupportsWSPrintv11>true</wprt11:SupportsWSPrintv11>
          </wprt:PrinterDescription>
        </wprt:ElementData>
      </wprt:PrinterElements>
    </wprt:GetPrinterElementsResponse>
  </soap:Body>
</soap:Envelope>
```

次の XML スニペットでは、Ws-print v1.1 をサポートしている印刷デバイス用のスキーマを示します。

```xml
<xs:schema targetNamespace="http://schemas.microsoft.com/windows/2010/06/wdp/printv11"
           xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11"
           xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified">

<xs:annotation>
    <xs:documentation>
        WS-Print Extensions for Driver Configuration and Consumable Definition
        Copyright 2010 Microsoft Corp. All rights reserved
    </xs:documentation>
</xs:annotation>

<xs:annotation>
    <xs:documentation> A Boolean element that denotes support for WS-Print V11 extensions
    </xs:documentation>
</xs:annotation>

<xs:element name="SupportsWSPrintv11" type="xs:boolean"/>
```

## <a name="specifying-ws-print-12-support"></a>WS 印刷 1.2 のサポートを指定します。


Ws-print 1.2 要素をサポートするプリンターは、その PrinterDescription wprtV12:SupportsWSPrintV12 を含めるを更新する必要があります。 WprtV12:SupportsWSPrintV12 でない場合は true に設定して指定し、WSDMon は要求しません Ws-print 1.2 要素プリンターから。

Ws-print v1.2 をサポートしている印刷デバイスは、Windows の名前空間内の他の要素をクエリするためには、その PrinterDescription で次の内容を含める必要があります。

```xml
<soap:Envelope
…
    xmlns:wprtV12="http://schemas.microsoft.com/windows/2012/10/wdp/printV12">
…
    <wprtV12:SupportsWSPrintV12>true</wprtV12:SupportsWSPrintV12>
…
</soap:Envelope>
```

次の XML スニペットは、WSD 印刷サービスの仕様の v1.2 から派生し、前のセクションで、コンテンツの適切な使用方法を示します。

```xml
<soap:Envelope
     xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
     xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
     xmlns:wprt="http://schemas.microsoft.com/windows/2006/08/wdp/print"
     xmlns:wprtV12="http://schemas.microsoft.com/windows/2012/10/wdp/printV12">
     <soap:Header>
          <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
          <wsa:Action>
               http://schemas.microsoft.com/windows/2006/08/wdp/print/GetPrinterElementsResponse
          </wsa:Action>
          <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
          <wsa:RelatesTo>uuid:MsgIdOfTheGetPrinterElementsRequest</wsa:RelatesTo>
     </soap:Header>
     <soap:Body>
         <wprt:GetPrinterElementsResponse>
            <wprt:PrinterElements>
             <wprt:ElementData Name="wprt:PrinterDescription" Valid="true">
                <wprt:PrinterDescription>
                     <wprt:ColorSupported>true</wprt:ColorSupported>
                         <wprt:DeviceId>MFG:Acme;MDL:PrintMaster 9020</wprt:DeviceId>
                         <wprt:MultipleDocumentJobsSupported>true</wprt:MultipleDocumentJobsSupported>
                     <wprt:PagesPerMinute>20</wprt:PagesPerMinute>
                     <wprt:PagesPerMinuteColor>8</wprt:PagesPerMinuteColor>
                     <wprt:PrinterName xml:lang="en-AU, en-CA, en-GB, en-US">
                             Accounting Printer in Copy Room 2</wprt:PrinterName>
                         <wprt:PrinterInfo xml:lang="en-AU, en-CA, en-GB, en-US">
                             Printer for use of Accounting only</wprt:PrinterInfo>
                         <wprt:PrinterLocation xml:lang="en-AU, en-CA, en-GB, en-US">
                             LA Campus – Building 3</wprt:PrinterLocation>                      
                         <wprtV12:SupportsWSPrintV12>true</wprtV12:SupportsWSPrintV12>
                    </wprt:PrinterDescription>
             </wprt:ElementData>
            </wprt:PrinterElements>
         </wprt:GetPrinterElementsResponse>
      </soap:Body>
</soap:Envelope>
```

スキーマの例を次の 3 つのセクションでは、Ws-print V1.1 で導入された新しい要素の一部を使用する方法を示します。 Ws-print V1.1 名前空間で導入されたすべての要素の詳細については、WS 印刷 v1.0 のサポート ファイルを参照してください。 – v1.2 に記載の**ダウンロード**セクション。

## <a name="enhanced-driver-configuration"></a>強化されたドライバーの構成


このスキーマは、このデバイスのデバイス固有 GPD または PPD 構成ファイルを提供します。

```xml
   <xs:annotation>
        <xs:documentation>Driver Configuration File definition</xs:documentation>
    </xs:annotation>
    <xs:element name="DriverConfiguration" type="wprt11:DriverConfigurationType"/>
    <xs:complexType name="DriverConfigurationType">
        <xs:sequence>
            <xs:element name="GPDConfigFile" type="xs:string" minOccurs="0" />
            <xs:element name="PPDConfigFile" type="xs:string" minOccurs="0" />
            <xs:any namespace="##other" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:anyAttribute namespace="##other" processContents="lax" />
    </xs:complexType>
```

## <a name="device-model-id"></a>デバイスのモデル ID


次のスキーマは、デバイスの ModelID をについて説明し、デバイス メタデータの取得のために使用します。 ModelIDs の詳細については、[ModelID 要素](https://msdn.microsoft.com/library/windows/hardware/ff549295.aspx)を参照してください。

```xml
    <xs:annotation>
        <xs:documentation> Print Device Model Id value for device differentiation</xs:documentation>
        <xs:documentation> Always represented as a GUID</xs:documentation>
    </xs:annotation>
    <xs:element name="DeviceModelId" type="wprt11:DeviceModelIdGuidType"/>
    <xs:simpleType name="DeviceModelIdGuidType">
        <xs:restriction base="xs:string">
            <xs:length value="36"/>
        </xs:restriction>
    </xs:simpleType>
```

## <a name="inktoner-color-representation-value"></a>インクまたはトナー色形式の値


次のスキーマは、特定のインクまたはトナー型の色を表す RGB triple を取得します。 この値は、アプリの UI に表示される色のより適切な表現を有効にすると、インクまたはトナーの消耗品を指定する必要があります。

```xml
    <xs:annotation>
        <xs:documentation>
            Ink/Toner Color Representation definition
            A 6-digit hex representation of the RGB color value this Consumable entry represents.
            Examples of these values are:
                Black – 000000
                Red – FF0000 
                White – FFFFFF
                Magenta – FF00FF
                Cyan – 00FFFF
                Yellow – FFFF00
                Blue – 0000FF
        </xs:documentation>    </xs:annotation>
    <xs:element name="ColorRepresentation" type="wprt11:ColorRepType"/>
    <xs:simpleType name="ColorRepType">
        <xs:restriction base="xs:string">
            <xs:length value="6"/>
        </xs:restriction>
    </xs:simpleType>
```

Ws-print v1.2 セクションで、このトピックで説明したように、次の新しい操作が Ws-print V1.2 名前空間に導入されました。

## <a name="setprinterelements"></a>SetPrinterElements


"SetPrinterElements"操作は、新しくして、クライアント プリンターのスキーマ要素の値を設定することができます。 SetPrinterElements 操作には、8 つの要素の要求と応答の 4 つの要素が必要があります。 要求と応答の要素では、クライアントにデータを挿入および WS 印刷デバイス スキーマ関連の取得を細かく制御を提供します。

たとえば、ElementPath データ要素 (SetPrinterElements 操作の一部) は XPath 文字列を設定するデータ要素のプリンター スキーマ内の場所を表すです。

SetPrinterElements 操作の詳細については、WS 印刷 v1.0 – ダウンロード セクションに記載バージョン 1.2 のサポート ファイルを参照してください。

## <a name="downloads"></a>ダウンロード


**仕様とサポート ファイルを Ws-print v1.0 – v1.2**

**ファイル:**[デバイスで Web サービスのデバイス定義 V1.0 を印刷](http://download.microsoft.com/download/E/9/7/E974CFCB-4B3B-40CC-AF92-4F7F84477F0B/Printer.zip)
**説明。** 2.64 Microsoft Word のドキュメントを格納しているとサポート ファイルは、MB zip ファイル2013 年 9 月 16 日

**仕様とサポート ファイル**

**ファイル:**[デバイスで Web サービスのデバイス定義 V1.0 を印刷](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PrintDevice.exe)
**説明。** 自己解凍形式のファイルは、Microsoft Word のドキュメントを含むファイルをサポートしている 76 KB2007 年 1 月 29 日

**ファイル:**[Web Services on Devices のサービス定義 V1.0 をスキャン](http://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/ScanService.zip)
**説明。**(1.5 MB zip ファイル Microsoft Word のドキュメントを格納しているとサポート ファイル。2012 年 2 月 9 日)

**ファイル:**[Web Services on Devices のデバイス定義 V1.0 をスキャン](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/ScanDevice.exe)
**説明。**(76 KB 自己解凍形式のファイルを Microsoft Word のドキュメントを格納していると、ファイルのサポート2007 年 1 月 29 日)
## <a name="related-topics"></a>関連トピック
[V4 プリンター ドライバーの接続](v4-printer-driver-connectivity.md)  



