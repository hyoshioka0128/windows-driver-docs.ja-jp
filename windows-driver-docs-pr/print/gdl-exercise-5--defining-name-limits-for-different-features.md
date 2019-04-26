---
title: GDL は、さまざまな機能を定義する名前の 5 つの制限を練習します。
description: GDL は、さまざまな機能を定義する名前の 5 つの制限を練習します。
ms.assetid: 8e6c59d7-c748-4133-ba70-e5be413bae54
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- テンプレートを定義する、WDK GDL という名前の制限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd23569edcce53cec862af2adbe17cb9352d546d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342588"
---
# <a name="gdl-exercise-5-defining-name-limits-for-different-features"></a>GDL 演習 5:さまざまな機能の名前の制限を定義する


### <a href="" id="exercise"></a> 演習

テンプレートを使用して[演習 4](gdl-exercise-4--defining-variants-of-constructs.md)、定義、\*名: コンス トラクター内に表示される、\*の一部である POption \*PFeature:InputTray 16 文字の最大数に制限されていますになるよう、\*名: 内で表示される、\*の一部である POption \*PFeature:用紙サイズは、24 文字の最大数に制限されます。

以前に定義されたテンプレートのいずれかの変更を削除または変更します。 エントリの適切な templatization を確認する単純な GDL データ ファイルを作成します。

### <a href="" id="solution"></a> ソリューション

次のテンプレートは、条件を満たします。

```cpp
*Template:  PAPER_SIZE_OPT_NAME
{
*Name:  "*Name"  *% isolate this branch from base templates
*Inherits: NAME
*MaxLength: 24 chars
}
*Template:  INPUTTRAY_OPT_NAME
{
*Name:  "*Name"  *% isolate this branch from base templates
*Inherits: NAME
*MaxLength: 16 chars
}

*Template:  INPUTTRAY_OPTION2
{
    *Inherits: INPUTTRAY_OPTION
    *Members:  (INPUTTRAY_OPT_NAME)
    *Instances:  <ANY>
}
*Template:  PAPERSIZE_OPTION2
{
    *Inherits: PAPERSIZE_OPTION
    *Members:  (PAPER_SIZE_OPT_NAME)
    *Instances:  <ANY>
}
*PFeature: random
{
*Name:"Generic Feature"
*DefaultOption: First
*POption: First
{
 *Name: "First Option"
 *Command: "Select me"
}
}
*PFeature: PaperSize
{
*Name: "Paper Size"
*DefaultOption: Letter
*POption: Letter
{
 *Name: "Letter"
 *Command: "Select Letter"
 *PaperSize: PAIR(8.5, 11) inches
}
*POption:   Legal
{
 *Name: "Legal"
 *Command: "Select Legal"
 *PaperSize: PAIR(8.5, 14) inches
}
*POption: A4
{
 *Name: "A4"
 *Command: "Select A4"
 *PaperSize: PAIR(205, 317) mm
}
}
*PFeature: InputTray
{
*Name:  "Paper Source"
*DefaultOption: Upper
*POption: Upper
{
 *Name: "Upper Tray"
 *Command:  "Select Upper Tray"
 *Capacity:  2000 sheets
}
*POption: Lower
{
 *Name: "Lower Tray"
 *Command:  "Select Lower Tray"
 *Capacity:  500 sheets
}
}
```

**注**   Using[継承](gdl-template-inheritance.md)、さらに改善し、以前のテンプレートのいずれかを変更することや、スキーマの目的は、兼ねてハッキングする. 基底クラスのバリエーションを派生させることができますを以前のテンプレート確立されます。 この機能は、継承の強度をもう 1 つです。 継承は、3 番目のパーティを変更するか、マスターのスキーマに違反してせずマスターのスキーマを拡張する機能を提供します。

 

 

 




