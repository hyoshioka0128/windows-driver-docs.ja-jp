---
title: 双方向通信スキーマ クエリの作成
description: 双方向通信スキーマ クエリの作成
ms.assetid: b18fc69a-652c-4e36-83b3-fc4715b03c0f
keywords:
- 双方向通信スキーマ WDK の印刷
- 双方向通信スキーマ WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13411cf556ba8ec1e96aeda0a7270aa07e3379b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550379"
---
# <a name="constructing-a-bidi-communication-schema-query"></a>双方向通信スキーマ クエリの作成


双方向通信のスキーマのクエリを構築する際に次の 3 つの点があります。

1.  クエリが始まり、`Printer`プロパティで、前に円記号が必要 (`\`)。

2.  クエリ内の任意のプロパティは、ピリオド文字で区切る必要があります (`.`)。

3.  値を親プロパティから、コロンで区切る必要があります、クエリには、値が含まれている場合 (`:`)。

### <a href="" id="example-request-and-response"></a> 要求と応答例

必要とされる XML クエリと応答の形式の例を次に、[双方向の通信インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545163)、IBidiSpl2 COM インターフェイスで具体的には。 最初の例は、2 つのスキーマを含む要求です。 最初のスキーマは、両面印刷ユニットがインストールされているかどうかを判断します。 2 つ目のスキーマは、ハード ディスクに関連付けられている値を決定します。

```cpp
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Configuration.DuplexUnit:Installed"/>
  <Query schema="\Printer.Configuration.HardDisk"/>
</bidi:Get>
```

次の例は、最初の例ではスキーマから一般的な応答のセットです。 最初の応答では、両面印刷ユニットがインストールされていることを示します。 残りの応答は、ハード ディスクがインストールされていることと、容量が 20 MB、うちが 10 MB 使用を示します。

```cpp
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Configuration.DuplexUnit:Installed">
    <Schema name="\Printer.Configuration.DuplexUnit:Installed">
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
  </Query>
  <Query schema="\Printer.Configuration.HardDisk">
    <Schema name="\Printer.Configuration.HardDisk:Installed">
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
    <Schema name="\Printer.Configuration.HardDisk:Capacity">
      <BIDI_INT>20</BIDI_INT>
    </Schema>
    <Schema name="\Printer.Configuration.HardDisk:FreeSpace">
      <BIDI_INT>10</BIDI_INT>
    </Schema>
  </Query>
</bidi:Get>
```

### <a href="" id="additional-query-examples"></a> 追加のクエリ例

一般的なタスクと関連付けられているクエリの一覧を次には。

<a href="" id="determine-whether-a-duplex-unit-is-installed-"></a>両面印刷ユニットがインストールされているかどうかを確認します。  
```cpp
\Printer.Configuration.DuplexUnit:Installed
```

<a href="" id="determine-which-input-bins-are-present-"></a>どの入力ビンが存在するかを決定します。  
```cpp
\Printer.Layout.InputBins
```

<a href="" id="determine-all-information-about-the-tray1-input-bin-"></a>トレイ 1 入力ビンに関するすべての情報を決定します。  
```cpp
\Printer.Layout.InputBins.Tray1
```

<a href="" id="determine-whether-the-tray1-input-bin-is-installed-"></a>トレイ 1 入力ビンがインストールされているかどうかを確認します。  
```cpp
\Printer.Layout.InputBins.Tray1:Installed
```

<a href="" id="determine-the-level-of-black-toner-identified-by--name--blk3e-"></a>識別される黒のトナーのレベルを決定する\[名前\]Blk3E します。  
```cpp
\Printer.Consumables.Blk3E:Level
```

<a href="" id="determine-the-level-of-fuser-oil-"></a>定着オイルのレベルを決定します。  
```cpp
\Printer.Consumables.FuserOil:Level
```

 

 




