---
title: 双方向通信スキーマ クエリを作成する
description: 双方向通信スキーマ クエリを作成する
ms.assetid: b18fc69a-652c-4e36-83b3-fc4715b03c0f
keywords:
- 双方向通信スキーマ WDK 印刷
- bidi 通信スキーマ WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f14581e557728897d1d7cdfa5e43962271a598df
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652857"
---
# <a name="constructing-a-bidi-communication-schema-query"></a>双方向通信スキーマ クエリを作成する


Bidi 通信スキーマクエリを構築する場合、次の3つの点に注意してください。

1.  クエリは `Printer` プロパティから始める必要があります。このプロパティの前には円記号 (`\`) を付ける必要があります。

2.  クエリ内のすべてのプロパティは、ピリオド文字 (`.`) で区切る必要があります。

3.  クエリに値が含まれている場合は、その親プロパティから値をコロン (`:`) で区切る必要があります。

### <a href="" id="example-request-and-response"></a>要求と応答の例

次に、 [bidi 通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)で必要とされる XML クエリと応答形式の例と、特に IBidiSpl2 COM インターフェイスの例を示します。 最初の例は、2つのスキーマを含む要求です。 最初のスキーマでは、双方向ユニットがインストールされているかどうかを判断します。 2番目のスキーマは、ハードディスクに関連付けられている値を決定します。

```cpp
<bidi:Get xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Configuration.DuplexUnit:Installed"/>
  <Query schema="\Printer.Configuration.HardDisk"/>
</bidi:Get>
```

次の例は、最初の例のスキーマからの一連の一般的な応答です。 最初の応答は、二重ユニットがインストールされていることを示します。 残りの応答は、ハードディスクがインストールされており、その容量が 20 MB であることを示しています。そのうち 10 MB は未使用です。

```cpp
<bidi:Get xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
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

### <a href="" id="additional-query-examples"></a>その他のクエリの例

一般的なタスクと関連付けられているクエリの一覧を次に示します。

<a href="" id="determine-whether-a-duplex-unit-is-installed-"></a>両面印刷ユニットがインストールされているかどうかを確認します。  
```cpp
\Printer.Configuration.DuplexUnit:Installed
```

<a href="" id="determine-which-input-bins-are-present-"></a>どの入力ビンが存在するかを判断します。  
```cpp
\Printer.Layout.InputBins
```

<a href="" id="determine-all-information-about-the-tray1-input-bin-"></a>Tray1 入力ビンに関するすべての情報を確認します。  
```cpp
\Printer.Layout.InputBins.Tray1
```

<a href="" id="determine-whether-the-tray1-input-bin-is-installed-"></a>Tray1 の入力ビンがインストールされているかどうかを確認します。  
```cpp
\Printer.Layout.InputBins.Tray1:Installed
```

<a href="" id="determine-the-level-of-black-toner-identified-by--name--blk3e-"></a>\[名\] Blk3E によって識別される黒のトナーのレベルを決定します。  
```cpp
\Printer.Consumables.Blk3E:Level
```

<a href="" id="determine-the-level-of-fuser-oil-"></a>フューザーオイルのレベルを決定します。  
```cpp
\Printer.Consumables.FuserOil:Level
```

 

 




