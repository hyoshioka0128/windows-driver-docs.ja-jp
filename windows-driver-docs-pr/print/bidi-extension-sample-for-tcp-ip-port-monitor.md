---
title: TCP/IP ポート モニターの双方向拡張機能サンプル
description: TCP/IP ポート モニターの双方向拡張機能サンプル
ms.assetid: 76454b0c-0e02-4372-97ed-2401a785cef8
keywords:
- 双方向の拡張機能は、WDK プリンター autoconfig をファイルします。
- ボックスの自動構成サポートの WDK プリンター、双方向の拡張ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dbcadbc5803c82c622f728ebbf3e390b8c602b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379264"
---
# <a name="bidi-extension-sample-for-tcpip-port-monitor"></a>TCP/IP ポート モニターの双方向拡張機能サンプル


次のコード例は、標準の TCP/IP ポート モニタの双方向通信のスキーマを拡張するサンプル XML ファイルです。

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<bidi:Schema xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
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

上記のコード サンプルは、次のクエリ結果します。

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
