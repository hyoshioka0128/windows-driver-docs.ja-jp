---
title: GPD ファイル エントリ形式
description: GPD ファイル エントリ形式
ms.assetid: 44057b4d-5ea1-426f-ae87-047b650cbf65
keywords:
- GPD ファイル エントリ WDK Unidrv の形式
- WDK GPD ファイルの形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 053581ba1a6e0ca48a780e3d82b8ffab649b2bc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570325"
---
# <a name="gpd-file-entry-format"></a>GPD ファイル エントリ形式





GPD ファイルのすべてのエントリは、次の形式に準拠しています。

**\\*** <em>EntryName</em>**:***EntryValue* **{**<em>GPD\_FileEntry, GPD\_FileEntry, ...</em>**}**

*EntryName*は常に Unidrv の GPD パーサーで認識する定義済みのキーワードの前にアスタリスクでします。

*EntryValue*のいずれかを指定する必要があります、 [GPD 値型](gpd-value-types.md)します。

各*GPD\_認証ファイル*は上記の形式に準拠している別の GPD ファイル エントリです。 これらのサブ項目の指定した有効なである必要があります*EntryName*のそれを含むエントリ。

いくつか*EntryName*キーワードは中かっこまたは含まれているサブ項目を受け入れません。

各 GPD エントリは行の終わりまたは右中かっこで終了 ( **}** )。

サブ項目が許されない、単純なの GPD ファイル エントリの例では、次の属性エントリを示します。

```cpp
*MaxCopies: 99
```

このエントリは、プリンターで処理できるコピーの最大数が 99 を指定します。

2 つのページの向き (縦または横) のいずれかのページを印刷できるプリンターを記述するより複雑な例を次に示します。 例には、それぞれの向きを選択するドライバーを送信する必要がありますコマンドも指定します。

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

 

 




