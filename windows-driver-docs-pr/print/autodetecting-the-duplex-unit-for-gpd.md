---
title: 両面印刷ユニット GPD の自動検出しています
description: 両面印刷ユニット GPD の自動検出しています
ms.assetid: a5c91b00-ca7c-4c22-a16c-a976011d8b89
keywords:
- 自動検出の両面印刷ユニット WDK のプリンターの自動構成
- GPD ファイル WDK GDL 拡張機能を両面印刷ユニットを自動検出しています
- ボックスの自動構成サポート WDK のプリンターが両面印刷ユニットを自動検出しています
- 両面印刷ユニットを検出します。
- 両面印刷ユニット WDK プリンターの自動構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13822ae9ded4430943a937ad182cfd383a3bb8e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535435"
---
# <a name="autodetecting-the-duplex-unit-for-gpd"></a>両面印刷ユニット GPD の自動検出しています


両面印刷ユニットにインストールできるようにする、GPD ファイルは次の例のように定義されている双方向機能にあるとします。

```GPD
*Feature: Duplex
{
   *rcNameID: =TWO_SIDED_PRINTING_DISPLAY
  *DefaultOption: NONE
  *Option: NONE
  {
    *rcNameID: =NONE_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.9
      *Cmd: "<1B>&l0S"
    }
  }
  *Option: VERTICAL
  {
    *rcNameID: =FLIP_ON_LONG_EDGE_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.10
      *Cmd: "<1B>&l1S"
    }
  }
  *Option: HORIZONTAL
  {
    *rcNameID: =FLIP_ON_SHORT_EDGE_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.10
      *Cmd: "<1B>&l2S"
    }
  }
}

*%
*% Installable Option
*%
*Feature: DuplexUnit
{
  *rcNameID: 429 *% Duplex Unit
  *HelpIndex: 12004
  *FeatureType: PRINTER_PROPERTY
  *DefaultOption: FALSE
  *Option: NotInstalled
  {
    *rcNameID: 444
    *DisabledFeatures: LIST(Duplex.VERTICAL, Duplex.HORIZONTAL)
  }
  *Option: Installed
  {
    *rcNameID: 443
  }
}
```

GDL の次のコード例では、(上記の GPD コード例で説明) する両面印刷ユニットが存在する自動検出する機能を提供し、適切なオプションを設定します。 この例では、スプーラーに表示されているクエリを送信、 \* **BidiQuery**を構築します。 プリンターでは、クエリを受信すると応答した可能性のある 2 つのいずれかの\***オプション**値を構築します。

```GDL
*Feature: DuplexUnit
{
  *% Note that the *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: DuplexUnit
  {
    *QueryString: "\Printer.Configuration.DuplexUnit:Installed"
  }

  *BidiResponse: DuplexUnit
  {
    *ResponseType: BIDI_BOOL
    *ResponseData: ENUM_OPTION(DuplexUnit)
  }

  *Option: NotInstalled
  {
    *BidiValue: BOOL(FALSE)
  }

  *Option: Installed
  {
    *BidiValue: BOOL(TRUE)
  }
}
```








