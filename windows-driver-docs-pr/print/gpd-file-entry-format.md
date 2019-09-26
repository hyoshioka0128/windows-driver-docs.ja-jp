---
title: GPD ファイル エントリ形式
description: GPD ファイル エントリ形式
ms.assetid: 44057b4d-5ea1-426f-ae87-047b650cbf65
keywords:
- GPD ファイルエントリ WDK Unidrv、形式
- WDK GPD ファイルのフォーマット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a47b967392c63bde1b8d476a1003168e592219d6
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285087"
---
# <a name="gpd-file-entry-format"></a>GPD ファイル エントリ形式





GPD ファイルのすべてのエントリは、次の形式に準拠しています。

\***EntryName:Entryvalue** {*GPD\_fileentry, GPD\_fileentry,...* }

*EntryName*は常に、UNIDRV の GPD パーサーが認識する事前定義されたキーワードで、前にアスタリスクが付いています。

*Entryvalue*は、 [GPD 値型](gpd-value-types.md)のいずれかである必要があります。

各*GPD\_fileentry*は、前に示した形式に準拠した、もう1つの GPD file エントリです。 これらのサブ項目は、それを含むエントリの指定された*EntryName*に対して有効である必要があります。

一部の*EntryName*キーワードでは、中かっこや、サブエントリを囲むことはできません。

各 GPD エントリは、行末または右中かっこ ( **}** ) で終了します。

サブ項目を受け付けない単純な GPD file エントリの例は、次の属性エントリです。

```cpp
*MaxCopies: 99
```

このエントリは、プリンターが処理できるコピーの最大数が99であることを指定します。

次に示すのは、2つのページの向き (縦または横) でページを印刷できるプリンターを記述する、より複雑な例です。 この例では、ドライバーが各向きを選択するために送信する必要のあるコマンドも指定します。

```cpp
*Feature: Orientation
{
    *Name: "Orientation"
    *DefaultOption: Portrait
    *Option: Portrait
    {
        *Name: "Portrait"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.7
            *Cmd: "<1B>&l0O"
        }
    }
    *Option: LANDSCAPE_CC90
    {
        *Name: "Landscape"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.7
            *Cmd: "<1B>&l1O"
        }
    }
}
```

 

 




