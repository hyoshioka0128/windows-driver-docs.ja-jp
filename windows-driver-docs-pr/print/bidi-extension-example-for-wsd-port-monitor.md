---
title: WSD ポート モニターの双方向拡張例
description: WSD ポート モニターの双方向拡張例
ms.assetid: a04f16d5-ae99-4df5-bb55-aef95bd03588
keywords:
- bidi 拡張ファイル WDK プリンター autoconfig
- 組み込み自動構成サポート WDK プリンター、bidi 拡張ファイル
- WSD スキーマ拡張の WDK プリンター
- スキーマ拡張の WDK WSD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e70f6eb1bda920791cf0d67181c9a9367ebaee
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652912"
---
# <a name="bidi-extension-example-for-wsd-port-monitor"></a>WSD ポート モニターの双方向拡張例

次のコード例は、Web Services for Devices (WSD) ポートモニターの bidi 通信スキーマを拡張するサンプル XML ファイルです。

```xml
<?xml version='1.0'?>
<bidi:Definition xmlns:bidi='https://schemas.microsoft.com/windows/2005/03/printing/bidi'>

  <Schema xmlns:nprt='https://schemas.microsoft.com/windows/2006/08/wdp/print'>
    <Property name='Printer'>
      <Property name='DeviceInfo'>
        <Value name='FriendlyName' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:PrinterName' type='BIDI_STRING' xmllang='true'/>
        <Value name='Location' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:PrinterLocation' type='BIDI_STRING' xmllang='true'/>
        <Value name='Comment' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:PrinterInfo' type='BIDI_STRING' xmllang='true'/>
        <Value name='IEEE1284DeviceId' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:DeviceId' type='BIDI_STRING'/>
      </Property>
      <Property name='Configuration'>
        <Property name='Memory'>
          <Value name='Size' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="RAM"]/nprt:Size' type='BIDI_INT' drvPrinterEvent='true'/>
          <Value name='PS' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="PSMemory"]/nprt:Size' type='BIDI_INT' drvPrinterEvent='true'/>
        </Property>
        <Property name='HardDisk'>
          <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="HardDisk"]' drvPrinterEvent='true'/>
          <Value name='Capacity' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="HardDisk"]/nprt:Size' type='BIDI_INT' drvPrinterEvent='true'/>
          <Value name='FreeSpace' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="HardDisk"]/nprt:Free' type='BIDI_INT' drvPrinterEvent='true'/>
        </Property>
        <Property name='DuplexUnit'>
          <Value name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:DuplexerInstalled' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
        </Property>
      </Property>
      <Property name='Consumables'>
        <Parameter name='$Name$' parameter='Name' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry/@nprt:Name'>
          <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]' drvPrinterEvent='true'/>
          <Value name='Type' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Type' type='BIDI_STRING' drvPrinterEvent='true'/>
          <Value name='Color' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Color' type='BIDI_STRING' drvPrinterEvent='true'/>
          <Value name='Level' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Level' type='BIDI_INT' drvPrinterEvent='true'/>
          <Value name='Model' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Model' type='BIDI_STRING' drvPrinterEvent='true'/>
        </Parameter>
      </Property>
      <Property name='Layout'>
        <Property name='NumberUp'>
          <Property name='PagesPerSheet'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:DocumentProcessing/nprt:NumberUp/nprt:PagesPerSheet' type='BIDI_INT' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:DocumentProcessing/nprt:NumberUp/nprt:PagesPerSheet/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
          <Property name='Direction'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:DocumentProcessing/nprt:NumberUp/nprt:Direction' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:DocumentProcessing/nprt:NumberUp/nprt:Direction/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
        </Property>
        <Property name='Orientation'>
          <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:DocumentProcessing/nprt:Orientation' type='BIDI_STRING' drvPrinterEvent='true'/>
          <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:DocumentProcessing/nprt:Orientation/nprt:AllowedValue' drvPrinterEvent='true'/>
        </Property>
        <Property name='InputBins'>
          <Parameter name='$TrayName$' parameter='TrayName' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry/@nprt:Name'>
            <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]' drvPrinterEvent='true'/>
            <Value name='MediaSize' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:MediaSize' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='MediaType' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:MediaType' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='MediaColor' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:MediaColor' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='FeedDirection' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:FeedDirection' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='Capacity' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:Capacity' type='BIDI_INT' drvPrinterEvent='true'/>
            <Value name='Level' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:Level' type='BIDI_INT' drvPrinterEvent='true'/>
          </Parameter>
        </Property>
      </Property>
      <Property name='Finishing'>
        <Value name='CollationSupported' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:CollationSupported' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
        <Value name='JogOffsetSupported' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:JogOffsetSupported' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
        <Property name='Staple'>
          <Value name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:StaplerInstalled' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
          <Property name='Location'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Location' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Location/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
          <Property name='Angle'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Angle' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Angle/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
        </Property>
        <Property name='HolePunch'>
          <Value name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:HolePunch/nprt:HolePunchInstalled' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
          <Property name='Pattern'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Pattern' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Pattern/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
          <Property name='Location'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Edge' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Edge/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
        </Property>
        <Property name='OutputBins'>
          <Parameter name='$TrayName$' parameter='TrayName' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry/@nprt:Name'>
            <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry[@nprt:Name="$TrayName$"]' drvPrinterEvent='true'/>
            <Value name='Capacity' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry[@nprt:Name="$TrayName$"]/nprt:Capacity' type='BIDI_INT' drvPrinterEvent='true'/>
            <Value name='Level' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry[@nprt:Name="$TrayName$"]/nprt:Level' type='BIDI_INT' drvPrinterEvent='true'/>
          </Parameter>
        </Property>
      </Property>
      <Property name='Status'>
        <Property name='Summary'>
          <Value name='State' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:PrinterState' type='BIDI_STRING'/>
          <Value name='StateReason' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:PrinterPrimaryStateReason' type='BIDI_STRING'/>
        </Property>
        <Property name='Detailed'>
          <Parameter name='Event$EventIndex$' parameter='EventIndex' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition/@nprt:Id'>
            <Value name='Name' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Name' type='BIDI_STRING'/>
            <Value name='Severity' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Severity' type='BIDI_STRING'/>
            <Property name='Component'>
              <Value name='Group' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Component/nprt:Group' type='BIDI_STRING'/>
              <Value name='Name' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Component/nprt:Name' type='BIDI_STRING'/>
            </Property>
          </Parameter>
        </Property>
      </Property>
    </Property>
  </Schema>
  <PortStatus>
    <Status>
      <Keyword>None</Keyword>
      <Code>0</Code>
      <Severity>0</Severity>
    </Status>
    <Status>
      <Keyword>AttentionRequired</Keyword>
      <Code>8</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>DoorOpen</Keyword>
      <Code>7</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MarkerFailure</Keyword>
      <ResourceIdOffset>0</ResourceIdOffset>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MarkerSupplyLow</Keyword>
      <Code>10</Code>
      <Severity>2</Severity>
    </Status>
    <Status>
      <Keyword>MarkerSupplyEmpty</Keyword>
      <Code>6</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MediaEmpty</Keyword>
      <Code>3</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MediaJam</Keyword>
      <Code>2</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MediaLow</Keyword>
      <ResourceIdOffset>1</ResourceIdOffset>
      <Severity>2</Severity>
    </Status>
    <Status>
      <Keyword>MediaNeeded</Keyword>
      <Code>5</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>OutputAreaAlmostFull</Keyword>
      <ResourceIdOffset>2</ResourceIdOffset>
      <Severity>2</Severity>
    </Status>
    <Status>
      <Keyword>OutputAreaFull</Keyword>
      <Code>4</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>Paused</Keyword>
      <ResourceIdOffset>3</ResourceIdOffset>
      <Severity>3</Severity>
    </Status>
  </PortStatus>
</bidi:Definition>
```

### <a name="description-of-schema-extension"></a>スキーマ拡張の説明

前の例の bidi 拡張ファイルには、ルート要素 &lt;定義&gt;が含まれており、2つの主要なセクションがあります。 &lt;スキーマ&gt;では、bidi スキーマ拡張が配置されます。もう1つは、ドライバーが WSD ステータスをポート &lt;情報&gt;3 ポートの状態構造 (\_ドキュメントで説明) にマップします。

スキーマ拡張で使用される名前空間は、Schema 要素で定義されている必要があります。 拡張機能の処理では、下位レベルの要素で定義されている名前空間は認識されません。 下位レベルの要素で名前空間を定義すると、拡張ファイルの検証に失敗します。

```xml
<Definition>
  <Schema>...</Schema>
  <PortStatus>...</PortStatus>
</Definition>
```

この拡張ファイルからの各 bidi クエリには次のものが含まれます。

-   WSD データから bidi データを作成する方法を説明するアルゴリズム。アルゴリズムは、 [Const](const.md)、 [Installed](installed.md)、 [List](list.md)、 [Value](value.md)の4つの構成要素を使用して定義できます。

-   WSD データを取得する方法を説明する WSD クエリパラメーター。

-   Bidi の結果を作成するために使用される WSD スキーマから特定の XML 要素をフィルター処理する XPath フィルター。

### <a name="parameter-construct"></a>パラメーターコンストラクター

前の例の bidi 拡張ファイルで使用される &lt;Parameter&gt; 要素は、次の形式のクエリを実行できるように、異なる値 (TopBin や BottomBin など) を受け取ることができる変数プロパティを定義します。

-   `\Printer.Layout.InputBins.TopBin:Installed`

-   `\Printer.Layout.InputBins.BottomBin:Installed`

次のクエリ例は、前の bidi 拡張で定義されているカスタム属性の使用方法を示しています。

```xml
<Property name='Printer'>
  <Property name='Layout'>
    <Property name='InputBins'>
      <Parameter name='$TrayName$'
        parameter='TrayName'
        query='wprt:PrinterConfiguration'
        filter='wprt:PrinterConfiguration/wprt:InputBins/wprt:InputBinEntry/wprt:Name'>
        <Installed
          name='Installed'
          query='wprt:PrinterConfiguration'
          filter='wprt:PrinterConfiguration/wprt:InputBins/wprt:InputBinEntry[wprt:Name="$TrayName$"]'/>
      </Parameter>
    </Property>
  </Property>
</Property>
```

前の例では、次のクエリが実行されます。

`\Printer.Layout.InputBins.[TrayName]:Installed`
