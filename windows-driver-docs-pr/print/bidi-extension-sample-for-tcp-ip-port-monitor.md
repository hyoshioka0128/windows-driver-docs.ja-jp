---
title: TCP/IP ポート モニターの双方向拡張機能サンプル
description: TCP/IP ポート モニターの双方向拡張機能サンプル
ms.assetid: 76454b0c-0e02-4372-97ed-2401a785cef8
keywords:
- bidi 拡張ファイル WDK プリンター autoconfig
- 組み込み自動構成サポート WDK プリンター、bidi 拡張ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c9f56681bb515ef57b391a69a28b8898ac9ed7d
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652880"
---
# <a name="bidi-extension-sample-for-tcpip-port-monitor"></a>TCP/IP ポート モニターの双方向拡張機能サンプル


次のコード例は、標準 TCP/IP ポートモニターの bidi 通信スキーマを拡張するサンプル XML ファイルです。

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<bidi:Schema xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
    <Property name="Printer">
      <Property name="Layout">
        <Property name="InputBins">
          <InputBin name="TopBin"    mibName="TRAY 1"/>
          <InputBin name="BottomBin" mibName="TRAY 2"/>
        </Property>
      </Property>
      <Property name="Finishing">
        <Property name="OutputBins">
          <OutputBin name="TopBin" mibName="Standard Bin"/>
        </Property>
      </Property>
      <Property name="Extension">
        <Property name="Version">
          <Const name="Major" type="BIDI_INT" value="1"/>
          <Const name="Minor" type="BIDI_INT" value="0"/>
        </Property>
        <Property name="System">
          <Value name="Name" type="BIDI_TEXT" oid="1.3.6.1.2.1.1.5"/>
        </Property>
        <Property name="DuplexUnit">
          <Installed name="Installed" oid="1.3.6.1.2.1.43.13.4.1.9"
                     deviceIndex="true">
            <Lookup value="3"/>
            <Lookup value="4"/>
          </Installed>
        </Property>
        <Property name="Channels">
          <Const name="Category" type="BIDI_STRING" value="Channels"/>
          <IndexedProperty name="Channel">
            <Value name="Type" oid="1.3.6.1.2.1.43.14.1.1.2" 
                   type="BIDI_STRING" deviceIndex="true"/>
          </IndexedProperty>
        </Property>
      </Property>
    </Property>
</bidi:Schema>
```

上記のコードサンプルでは、次のクエリが実行されます。

```cpp
\Printer.Layout.InputBins.TopBin:Installed
\Printer.Layout.InputBins.TopBin:Level
\Printer.Layout.InputBins.TopBin:MediaSize
\Printer.Layout.InputBins.TopBin:MediaType
\Printer.Layout.InputBins.BottomBin:Installed
\Printer.Layout.InputBins.BottomBin:Level
\Printer.Layout.InputBins.BottomBin:MediaSize
\Printer.Layout.InputBins.BottomBin:MediaType
\Printer.Finishing.OutputBins.TopBin:Installed
\Printer.Finishing.OutputBins.TopBin:Level
\Printer.Extension.Version:Major
\Printer.Extension.Version:Minor
\Printer.Extension.System:Name
\Printer.Extension.DuplexUnit:Installed
\Printer.Extension.Channels:Category
\Printer.Extension.Channels.Channel001:Type
```
