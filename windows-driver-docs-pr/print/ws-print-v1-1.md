---
title: Web Services on Devices for Printing (WS-Print)
description: 印刷用のデバイスの Web サービス (WS 印刷) は、Windows Vista で導入され、印刷とスキャンの周辺機器用の接続プロトコルを提供します。
ms.assetid: 4A641EF8-FBD3-46CA-9284-28AF1A4B8226
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6231bc8dadeae49a12d2880620b99b8b8606f054
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881928"
---
# <a name="web-services-on-devices-for-printing-ws-print"></a>Web Services on Devices for Printing (WS-Print)

印刷用のデバイスの Web サービス (WS 印刷) は、Windows Vista で導入され、印刷とスキャンの周辺機器用の接続プロトコルを提供します。

## <a name="overview"></a>概要

Web サービステクノロジは、情報を記述および共有するための共通のフレームワークを提供します。 その結果、Windows には、ネットワークに接続されたデバイスでサービスを使用および制御するための一連のプロトコルが用意されています。

印刷およびスキャン用に4つの Web サービス仕様が存在します。これは、デバイスの製造元が Windows でのデバイスの接続、インストール、および使用に関する改善されたカスタマーエクスペリエンスを活用するのに役立ちます。

## <a name="ws-print-v11"></a>WS 印刷 v1.1

Windows 8 では、web services on devices (WSD) の印刷スキーマが v1.1 に更新されました。 このバージョンのスキーマ (WS-RELIABLEMESSAGING v1.1 と呼ばれます) は、強化されたドライバー構成、インク/トナーの色表現の向上、およびデバイスモデル Id をサポートするように更新されました。

## <a name="ws-print-v12"></a>WS-RELIABLEMESSAGING 1.2

Windows 8.1 の場合、WS-ATOMICTRANSACTION には、WS-ATOMICTRANSACTION で使用されるすべての操作とスキーマ要素が含まれていますが、デバイス上の web サービスの印刷サービス定義が更新されました。 また、印刷用のデバイス上の新しい Web サービスは、WS-RELIABLEMESSAGING v1.0 です。

では、新しいスキーマ要素がサポートされ、新しい操作が追加されました。 新しい schema 要素 "SupportsWSPrintV12" を使用して、WS 印刷 v1.0 のサポートを識別します。 新しい操作 "Setprinter Elements" を使用すると、クライアントはプリンター上の schema 要素の値を設定できます。 たとえば、クライアントは、プリンターがインクジェットのヘッドを再調整するために使用する "Inkヘッドの配置値" というカスタム要素を設定できます。

ここでは、必要に応じて、[ダウンロード] セクションで、完全なスタンドアロン形式で、関連付けられている Web サービス記述言語 (Wsdl) と XML スキーマ定義 (Xsd) の仕様を提供しています。 これら4つのデバイス上の Web サービスの仕様は、Windows driver development kit (WDK) を参照する、付属の技術文書使用許諾契約書に記載されています。

以下のセクションでは、WS 印刷のさまざまな側面について詳しく説明します。

## <a name="sequence-diagrams"></a>シーケンス図

次のシーケンス図は、サポートされている WS 印刷名前空間のバージョンを判断し、拡張されたスキーマ要素を取得するために、クライアントとプリンター間の相互作用を示しています。

### <a name="ws-print-v11-sequence-diagram"></a>WS-RELIABLEMESSAGING v1.1 シーケンス図

次に、WS-ATOMICTRANSACTION をサポートするプリンターの相互作用シーケンス図を示します。

![クライアントとプリンターの間の相互作用と、プリンターの説明と構成に関するその後のクエリを示すシーケンス図。](images/wsprint-diagv11.png)

プリンターが WS-RELIABLEMESSAGING v1.1 をサポートしている場合、クライアントからの Getprinter Elements (wprt: プリンターの説明) クエリに応答して、プリンターは、そのことを示すために情報を送り返します。

プリンターが WS Print v1.1 をサポートしていることを確認すると、クライアントは Getprinter Elements (wprt11: DriverConfiguration) クエリを送信し、プリンターは要求されたドライバー構成情報で応答します。

### <a name="ws-print-v12-sequence-diagram"></a>WS-RELIABLEMESSAGING v1.0 のシーケンス図

次に、WS-I 1.2 をサポートするプリンターの相互作用シーケンス図を示します。

![クライアントとプリンターの間の相互作用と、プリンターの説明と構成に関する次のクエリを示すシーケンス図。](images/wsprint-diagv12.png)

プリンターで WS-ATOMICTRANSACTION がサポートされている場合、クライアントからの Getprinter Elements (wprt: プリンターの説明) クエリに応答して、プリンターは、そのことを示すために情報を送り返します。

さらに、Getprinter Elements (wprt: wprt12) 呼び出しに応答して、プリンターは SupportsWSPrintV12: を返します。 その後、クライアントは、Setprint Elements 操作を呼び出して、WS 印刷デバイスでサポートされているスキーマに1つ以上のデータ要素を設定できます。

プリンターが WS-RELIABLEMESSAGING v1.0 をサポートしていることを確認すると、クライアントは Getprinter Elements (wprt12: DriverConfiguration) クエリを送信し、プリンターは要求されたドライバー構成情報で応答します。

## <a name="namespaces"></a>名前空間

### <a name="ws-print-v11-namespace"></a>WS-RELIABLEMESSAGING v1.1 名前空間

**名前空間:** `<http://schemas.microsoft.com/windows/2010/06/wdp/printv11>`
**XML 名前空間の定義:** `xmlns:wprt12="<http://schemas.microsoft.com/windows/2012/10/wdp/printV12>"`

### <a name="ws-print-v12-namespace"></a>WS-ATOMICTRANSACTION の名前空間

**名前空間:** `<http://schemas.microsoft.com/windows/2012/10/wdp/printV12>`
**XML 名前空間の定義:** `xmlns:wprt11="<http://schemas.microsoft.com/windows/2010/06/wdp/printv11>"`

## <a name="specifying-ws-print-11-support"></a>WS Print 1.1 サポートの指定

WS Print 1.1 要素をサポートするプリンターでは、wprt11: SupportsWSPrintv11 を含めるようにプリンターの説明を更新する必要があります。 Wprt11: SupportsWSPrintv11 が指定されておらず、true に設定されている場合、WSDMon はプリンターからの WS Print 1.1 要素を要求しません。

WS-ATOMICTRANSACTION をサポートする印刷デバイスでは、Windows がその名前空間の他の要素に対してクエリを実行するために、プリンターの説明に次の内容を含める必要があります。

```xml
<soap:Envelope
...
  xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
...
  <wprt11:SupportsWSPrintv11>true</wprt11:SupportsWSPrintv11>
...
```

次の XML スニペットは、WSD Print Service Specification v1.0 から派生したもので、前のセクションでコンテンツが適切に使用されていることを示しています。

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

次の XML スニペットは、WS-RELIABLEMESSAGING v1.1 をサポートする印刷デバイスのスキーマを示しています。

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

## <a name="specifying-ws-print-12-support"></a>WS Print 1.2 サポートの指定

WS Print 1.2 要素をサポートするプリンターでは、wprtV12: SupportsWSPrintV12 を含めるようにプリンターの説明を更新する必要があります。 WprtV12: SupportsWSPrintV12 が指定されておらず、true に設定されている場合、WSDMon はプリンターからの WS Print 1.2 要素を要求しません。

WS-ATOMICTRANSACTION をサポートする印刷デバイスでは、Windows がその名前空間の他の要素に対してクエリを実行するために、プリンターの説明に次の内容を含める必要があります。

```xml
<soap:Envelope
…
    xmlns:wprtV12="http://schemas.microsoft.com/windows/2012/10/wdp/printV12">
…
    <wprtV12:SupportsWSPrintV12>true</wprtV12:SupportsWSPrintV12>
…
</soap:Envelope>
```

次の XML スニペットは、WSD Print Service Specification v1.1 から派生したもので、前のセクションで説明した内容の適切な使用方法を示しています。

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

次の3つのセクションのスキーマ例では、WS-RELIABLEMESSAGING v1.1 で導入されたいくつかの新しい要素の使用方法を示しています。 WS Print v1.1 名前空間で導入されたすべての要素の詳細については、以下の**ダウンロード**セクションに記載されている、「サポートファイル」を参照してください。

## <a name="enhanced-driver-configuration"></a>拡張ドライバーの構成

このスキーマは、デバイス固有の GPD または PPD 構成ファイルをこのデバイスに提供します。

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

## <a name="device-model-id"></a>デバイスモデル ID

次のスキーマは、デバイスの ModelID を記述し、デバイスメタデータの取得に使用されます。 ModelIDs の詳細については、「 [Modelids 要素](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))」を参照してください。

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

## <a name="inktoner-color-representation-value"></a>インク/トナーの色の表記値

次のスキーマは、特定のインクまたはトナーの種類の色を表す RGB トリプルを取得します。 この値は、アプリケーション UI に表示される色をより適切に表現できるように、インクまたはトナー消耗品に対して指定する必要があります。

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

このトピックで既に説明したように、「WS-ATOMICTRANSACTION v2.0」セクションでは、次の新しい操作が WS-Print v1.0 名前空間で導入されました。

## <a name="setprinterelements"></a>Setプリンター要素

**Setprinter elements**操作は新しいもので、クライアントはプリンター上の schema 要素の値を設定できます。 Setの Elements 操作には、8つの要求要素と4つの応答要素があります。 要求要素と応答要素を使用すると、クライアントは、WS 印刷デバイススキーマとの接続でデータの挿入と取得を細かく制御できます。

たとえば、ElementPath データ要素 (Setprinter Elements 操作の一部) は、設定するデータ要素のプリンタースキーマ内の場所を表す XPath 文字列です。

Setprint Elements 操作の詳細については、後述の「**ダウンロード**」セクションに記載されている「ws-i v1.0-v1.0 のサポートファイル」を参照してください。

## <a name="downloads"></a>ダウンロード

### <a name="specification-and-supporting-files-for-ws-print-v10--v12"></a>WS プリント v1.0-v1.0 の仕様とサポートファイル

**File:** デバイス[上の Web サービスの印刷デバイス定義](https://download.microsoft.com/download/E/9/7/E974CFCB-4B3B-40CC-AF92-4F7F84477F0B/Printer.zip)V1.0
**説明:** Microsoft Word 文書とサポートファイルを含む 2.64 MB の zip ファイル2013年9月16日

### <a name="specification-and-supporting-files"></a>仕様とサポートファイル

**File:** デバイス[上の Web サービス用にデバイス定義 v1.0 を印刷](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PrintDevice.exe)
**説明:** 76 KB 自己解凍形式の Microsoft Word 文書とサポートファイルを含むファイル。2007年1月29日

**ファイル:** [デバイス上の Web サービスのサービス定義 v1.0 をスキャン](https://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/ScanService.zip)
**説明:** (Microsoft Word 文書とサポートファイルを含む 1.5 MB の zip ファイル。2012年2月9日)

**ファイル:** デバイス[の Web サービス用にデバイス定義 v1.0 をスキャン](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/ScanDevice.exe)
**説明:** (76 KB 自己解凍形式のファイルを含む Microsoft Word 文書とサポートファイルを含む)2007年1月29日)

## <a name="related-topics"></a>関連トピック

[V4 プリンタードライバーの接続](v4-printer-driver-connectivity.md)  
