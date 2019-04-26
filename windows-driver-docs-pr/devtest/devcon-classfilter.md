---
title: DevCon ClassFilter
description: 追加、削除、表示、およびデバイス セットアップ クラスに対するドライバーのフィルターの順序を変更します。 ローカル コンピューターでのみ有効です。
ms.assetid: c04200c7-2897-46bd-ac5f-f838efef79d9
keywords:
- DevCon ClassFilter ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon ClassFilter
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f8d1d2ebb83c1548a08560d244709a1f9db5bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360098"
---
# <a name="devcon-classfilter"></a>DevCon ClassFilter


追加、削除、表示、およびデバイス セットアップ クラスに対するドライバーのフィルターの順序を変更します。 ローカル コンピューターでのみ有効です。

```
    devcon classfilter class {upper | lower} [ = | @driver | -driver | +driver | !driver ]...
```

## <a name="span-idddkdevconclassfiltertoolsspanspan-idddkdevconclassfiltertoolsspanparameters"></a><span id="ddk_devcon_classfilter_tools"></span><span id="DDK_DEVCON_CLASSFILTER_TOOLS"></span>パラメーター


<span id="_______class______"></span><span id="_______CLASS______"></span> *class*   
デバイス セットアップ クラスを指定します。

<span id="_______upper______"></span><span id="_______UPPER______"></span> **上限**   
指定したドライバーが上位クラス フィルター ドライバーを示します。

<span id="_______lower______"></span><span id="_______LOWER______"></span> **低い**   
指定したドライバーが低いクラス フィルター ドライバーを示します。

<span id="______________"></span> **=**   
(前に、最初のドライバー) フィルター ドライバーの一覧の先頭にカーソルを移動します。

<span id="________driver______"></span><span id="________DRIVER______"></span> **@**<em>ドライバー</em>   
指定されたドライバーの次のインスタンス上にカーソルを配置します。

<span id="-driver"></span><span id="-DRIVER"></span>**-* * * ドライバー*  
前に追加します。 カーソルが配置されているドライバーの前に指定されたドライバーを挿入します。

ドライバーには、カーソルが配置されていない、DevCon は一覧の先頭に指定されたドライバーを挿入します。 サブコマンドが完了したら、カーソルは、新しく追加されたドライバーにします。

<span id="________driver______"></span><span id="________DRIVER______"></span> **+**<em>ドライバー</em>   
後に追加します。 カーソルが配置されているドライバーの後に指定されたドライバーを挿入します。

ドライバーには、カーソルが配置されていない、DevCon はリストの最後に、指定したドライバーを挿入します。 サブコマンドが完了したら、カーソルは、新しく追加されたドライバーにします。

<span id="________driver______"></span><span id="________DRIVER______"></span> **!**<em>ドライバー</em>   
一覧から、指定したドライバーの次の出現を削除します。

サブコマンドが完了したら、カーソルは、削除されたドライバーの位置を占有します。 その後**+** または**-** サブコマンドは、カーソル位置にある新しいドライバーを挿入します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

A **DevCon ClassFilter**コマンドは、演算子で構成される 1 つまたは複数のサブコマンドを含めることができます (**=**、 **@**、  **-**、 **+**、 **!**) とフィルター ドライバーの名前。 DevCon は、コマンド内で出現する順序で、サブコマンドを実行します。

サブコマンドせず、 **DevCon ClassFilter**コマンドは、指定したクラスに上限や下限のフィルター ドライバーを表示します。 たとえば、 **devcon classfilter net 低い**Net セットアップ クラスの下のフィルター ドライバーが表示されます。

**DevCon ClassFilter**操作では、仮想のカーソルを使用して、クラスのフィルター ドライバーの一覧を移動します。 カーソルは、最初のドライバーの一覧で前に、フィルター ドライバーの一覧の先頭から開始されます。 返されない限り、開始位置にカーソルは常に、フィルター ドライバーの一覧を移動フォワード DevCon サブコマンドの実行時にします。

サービスとして、ドライバーがインストールされていない場合、DevCon がクラスにフィルター ドライバーを追加できません、つまり、ある必要があります、ドライバーのレジストリ サブキー、 [HKLM\\システム\\CurrentControlSet\\サービス](https://msdn.microsoft.com/library/windows/hardware/ff546188)レジストリ キー。 このセーフガードから誤ってが存在しないフィルター ドライバーを追加し、それによってレンダリング システムを起動できなくすることはできません。

使用して、フィルター ドライバーの変更は、デバイスを再起動する必要があるため、 [ **DevCon 再起動**](devcon-restart.md)コマンドを含めたり、 **/r** で(再起動が条件付き)パラメーター**DevCon ClassFilter**コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon classfilter mouse upper
devcon /r classfilter mouse upper !mouclass +newmou
devcon /r classfilter net lower @netfltr -testfltr
devcon /r classfilter volume upper !volsnap =!volsnap2
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[23 の使用例:セットアップ クラスに対するドライバーだけを表示します。](devcon-examples.md#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[24 の使用例:フィルター ドライバー セットアップ クラスを追加します。](devcon-examples.md#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[25 の使用例:[クラス] 一覧で、フィルター ドライバーを挿入します。](devcon-examples.md#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[26 の使用例:フィルター ドライバーを置き換える](devcon-examples.md#ddk_example_26_replace_a_filter_driver_tools)

[27 の使用例:フィルター ドライバーの順序を変更します。](devcon-examples.md#ddk_example_27_change_the_order_of_filter_drivers_tools)









