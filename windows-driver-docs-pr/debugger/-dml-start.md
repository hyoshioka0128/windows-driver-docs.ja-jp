---
title: .dml_start (表示 DML の開始ポイント)
description: .Dml_start コマンドでは、デバッガーのマークアップ言語 (DML) をサポートするコマンドを使用した探索の開始点として機能する出力が表示されます。
ms.assetid: 1CFCACDC-B253-4E9B-9877-EE9F1E91395F
keywords:
- .dml_start (表示 DML の開始ポイント) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dml_start (Display DML Starting Point)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7fae322482beeb1624a1facc33185954cdc5df8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530314"
---
# <a name="dmlstart-display-dml-starting-point"></a>.dml\_開始 (DML の開始点の表示)


**.Dml\_開始**コマンドには、探索を使用してコマンドをサポートするために、開始点として機能する出力が表示されます。[デバッガー Markup Language](debugger-markup-language-commands.md) (DML)。

```dbgcmd
.dml_start
.dml_start filename
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="filename"></span><span id="FILENAME"></span>*ファイル名*  
開始の出力として表示される DML ファイルの名前。

## <a name="span-idusingthedefaultstartingoutputspanspan-idusingthedefaultstartingoutputspanspan-idusingthedefaultstartingoutputspanusing-the-default-starting-output"></a><span id="Using_the_Default_Starting_Output"></span><span id="using_the_default_starting_output"></span><span id="USING_THE_DEFAULT_STARTING_OUTPUT"></span>既定の出力の開始を使用します。


場合*filename*は省略すると、デバッガーを表示する既定の DML 開始出力次の図のようにします。

![.dml のスクリーン ショット\-出力の開始](images/dmlstart01.png)

前の例の出力の各行は、他のコマンドを呼び出すクリックできるリンクです。

## <a name="span-idprovidingadmlfilespanspan-idprovidingadmlfilespanspan-idprovidingadmlfilespanproviding-a-dml-file"></a><span id="Providing_a_DML_File"></span><span id="providing_a_dml_file"></span><span id="PROVIDING_A_DML_FILE"></span>DML ファイルを提供します。


DML ファイルへのパスを指定する場合、ファイルは、開始の出力として使用されます。 たとえば、ファイル c:\\MyFavoriteCommands.txt には、次のテキストと DML タグが含まれています。

```dbgcmd
Display all device nodes.
   <link cmd="!devnode 0 1">!devnode 0 1</link>

Display all device nodes that are driven by a specified service.
Include child nodes in the display.
   <b>!devnode 0 1</b> <i>ServiceName</i>  
   Example: <link cmd="!devnode 0 1 usbehci">!devnode 0 1 usbehci</link>

Explore device stacks, device objects, and driver objects.
   <b>!devstack</b>  List the device objects in a device stack.
   <b>!devobj</b>    Display information about a device object.
   <b>!drvobj</b>    Display information about a driver object.
```

コマンドは、 **.dml\_c: 開始\\MyFavoriteCommands.txt**次の図のように、ファイルが表示されます。

![dml ファイル出力のスクリーン ショット](images/dmlstart02.png)

<a name="remarks"></a>注釈
-------

DML ファイルで使用できる DML タグについては、Windows のツールのデバッグの dml.doc のインストール フォルダーを参照してください。

多くの場合、出力する DML の動作でも、[コマンド ブラウザー ウィンドウ](command-browser-window.md)します。 コマンドのブラウザーのウィンドウで DML ファイルを表示する使用 **.browse .dml\_開始** *filename*します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[デバッガーのマークアップ言語コマンド](debugger-markup-language-commands.md)

[**.browse**](-browse--display-command-in-browser-.md)

 

 






