---
title: 仮想テンプレートから GDL 演習 2 の継承
description: 仮想テンプレートから GDL 演習 2 の継承
ms.assetid: 89878438-bea4-4d6f-bf3b-88d5bef0e6ab
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- スキーマ WDK GDL、GDL スキーマを実装します。
- WDK GDL、継承のテンプレート
- WDK GDL、例のテンプレート
- WDK GDL の継承
- 仮想テンプレート WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 530c5f3606da5bebbac7cbba59a25a5fd6470484
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369797"
---
# <a name="gdl-exercise-2-inheriting-from-virtual-templates"></a>GDL 演習 2:仮想テンプレートから継承する


### <a href="" id="exercise"></a> 演習

1 の Unicode 文字を表現する 2 バイトを使用してエンコードされた Unicode 文字列を受け取るデータ型を定義します。 次に、以前に定義された仮想テンプレートから継承する非仮想テンプレートを定義します。 作成したスキーマを変更しないでください[演習 1](gdl-exercise-1--implementing-a-gdl-schema.md)します。 サンプル GDL データ ファイルを作成し、スキーマが正しく適用されることを確認します。 スキーマに準拠し、エラーが検出されたことを確認サンプル GDL データ ファイルを作成します。

### <a href="" id="solution"></a> ソリューション

次の 2 つのテンプレートは、Unicode データ型を定義します。

```cpp
*Include: MasterTemplate.gdl
 
*Template:  XML_STRING
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "string"
}
```

```cpp
*Template:  NORMAL_STRING
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "NORMAL_STRING"
}
```

次のテンプレートは、演習 1 で定義されているテンプレートから継承します。 名前付きコンストラクトが\*コマンドと 3 つの種類の属性。**\*名前**(表示される、ルート レベルで)、  **\*CommandName** (内で表示されることができます、\*コマンド コンストラクト)、および **\*UniName** (することができます表示される両方のコンテキスト内で)。

```cpp
*Template:  COMMAND
{
    *Name:  "*Command"
    *Inherits: CONSTRUCTS
    *Instances:  <ANY>
}
*Template:  ROOT_NAME
{
    *Name:  "*Name"
    *Inherits: ROOT_ATTRIB
    *ValueType:  NORMAL_STRING
}
*Template:  CMD_NAME
{
    *Name:  "*CommandName"
    *Inherits: CONSTRUCT_ATTRIB
    *ValueType:  NORMAL_STRING
}
*Template:  UNIVERSAL_NAME
{
    *Name:  "*UniName"
    *Inherits: FREEFLOAT
    *ValueType:  NORMAL_STRING
}
```

次の GDL ファイルは、指定したスキーマに準拠します。

```cpp
*Name: "can only appear at root level"
*UniName:  "can appear anywhere"
*Command: X
{
    *CommandName:  "May only appear within a command"
    *UniName:  "can appear anywhere, even in a command"
    *Command: nested
    {
        *CommandName:  "nested commands are ok."
        *UniName:  "template defined a recursive nesting" 100 %
    }
}
```

次の GDL ファイルは、特定のスキーマに準拠していません。

```cpp
*CommandName:  "Error! May only appear within a command"
*Command: X
{
    *Name: "Error! can only appear at root level"
}
```

 

 




