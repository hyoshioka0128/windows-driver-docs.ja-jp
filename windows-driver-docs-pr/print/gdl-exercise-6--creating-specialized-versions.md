---
title: 特殊化されたバージョンを GDL 手順 6 を作成します。
description: 特殊化されたバージョンを GDL 手順 6 を作成します。
ms.assetid: d9e60958-58b6-4ffe-a955-bc1b13b6a649
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- WDK GDL、特殊なバージョンの作成を構築します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f62f1c624cbec11cb4665e1c0c3cbae514b34c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375601"
---
# <a name="gdl-exercise-6-creating-specialized-versions"></a>GDL 演習 6:特殊なバージョンを作成する


### <a href="" id="exercise"></a> 演習

使用して[演習 5](gdl-exercise-5--defining-name-limits-for-different-features.md)、3 つの特殊なバージョンを作成する\*の POption \*PFeature:ここをクリックします。

-   最初のバージョンでは、'文字'、'有効' および 'A4' のインスタンスの名前を持つ Papersize オプションです。 これらのオプションは、現在の動作があります。

-   2 番目のバージョンは 'Custom' のインスタンスの名前を持つ Papersize オプションについては、次の追加属性が認識されます。**\*MinSize**と **\*MaxSize**します。

-   3 番目のバージョンは OEM が定義されているし、追加の属性が認識に考慮されるその他の用紙サイズ オプションを取り上げます。**\*OEM\_情報**します。

以前に定義されたテンプレートのいずれかの変更を削除または変更します。 エントリの適切な templatization を確認する単純な GDL データ ファイルを作成します。

### <a href="" id="solution"></a> ソリューション

次のコード例では、1 つの解答を示します。

```cpp
*Template:  MIN_SIZE
{
    *Name: "*MinSize"
    *Type:  ATTRIBUTE
    *ValueType:  PAGE_DIM
}
*Template:  MAX_SIZE
{
    *Name: "*MaxSize"
    *Type:  ATTRIBUTE
    *ValueType:  PAGE_DIM
}

*Template:  OEM_INFO
{
    *Name: "*OEM_Info"
    *Type:  ATTRIBUTE
    *ValueType:  NORMAL_STRING
}


*Template:  OEM_PAPERSIZE_OPTION
{
    *Inherits: PAPERSIZE_OPTION2
    *Members:  (OEM_INFO)
    *Instances:  <ANY>
}
*Template:  CUST_PAPERSIZE_OPTION
{
    *Inherits: PAPERSIZE_OPTION2
    *Members:  (MIN_SIZE, MAX_SIZE)
    *Instances:  Custom
}
*Template:  PREDEFINED_PAPERSIZE_OPTION
{
    *Inherits: PAPERSIZE_OPTION2
    *Instances:  (Letter, Legal, A4)
}
```

次のコード例では、検証のためのサンプル GDL データ ファイルを示します。

```cpp
*PFeature: random
{
    *Name:  "Generic Feature"
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
        *PaperSize: PAIR(8.5, 11) ,  inches
    }
    *POption:   Legal
    {
        *Name: "Legal"
        *Command: "Select Legal"
        *PaperSize: PAIR(8.5, 14) ,  inches
    }
    *POption: A4
    {
        *Name: "A4"
        *Command: "Select A4"
        *PaperSize: PAIR(205, 317),  mm
    }
    *POption: OEMName_Special_size
    {
        *Name: "OEMName size"
        *Command: "Select OEMName size"
        *PaperSize: PAIR(365, 487), mm
        *OEM_Info: "<83 d4 93 ae>"
    }

    *POption: Custom
    {
        *Name: "Custom Size"
        *Command: "Select Custom"
        *MaxSize: PAIR(400, 500), mm
        *MinSize: PAIR(100, 150), mm
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
        *Capacity:  2000  *% sheets
    }
    *POption: Lower
    {
        *Name: "Lower Tray"
        *Command:  "Select Lower Tray"
        *Capacity:  500 *% sheets
    }
}
```

 

 




