---
title: TVOT\_スクロール バー
description: TVOT\_スクロール バー
ms.assetid: 8d905933-9629-48eb-9130-afa3dfa15099
keywords:
- TVOT_SCROLLBAR 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_SCROLLBAR
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f61b413adeb72bdfcb89c50d9a510d7d49e5024
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575098"
---
# <a name="tvotscrollbar"></a>TVOT\_スクロール バー


## <span id="ddk_tvot_scrollbar_gg"></span><span id="DDK_TVOT_SCROLLBAR_GG"></span>


TVOT\_グループ ボックス内のスクロール バーのスクロール バー オプションの種類で構成されます。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
現在のスクロール バーの位置を表す値。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)構造体の配列 (**pOptParam**のメンバー [ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**スクロール バーの単位を識別するテキストの NULL で終わる文字列を指します。

**pOptParam**\[1\]-&gt;**pData**スクロール バーの範囲の下限を説明するテキストの NULL で終わる文字列を指します。

**pOptParam**\[2\]-&gt;**pData**スクロール バーの範囲の上限を記述するテキストの aNULL で終わる文字列を指します。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**スクロール バーに関連付けるアイコンを識別します。

**pOptParam**\[1\]-&gt;**IconID**スクロール バーの範囲の下限を表す 16 ビット符号付きの値を指定します。

**pOptParam**\[2\]-&gt;**IconID**その値が表示される前に、選択したスクロールの位置に適用される mulitplication 係数を指定します。 (通常は、この値は 1 です。)

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
**pOptParam**\[0\]-&gt;**lParam**は使用されません。

**pOptParam**\[1\]-&gt;**lParam**スクロール バーの範囲の上限を表す 16 ビット符号付きの値を指定します。

**pOptParam**\[2\]-&gt;**lParam**スクロールの増分値を指定します。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**型**  
TVOT\_スクロール バー

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**カウント**  
3

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**スタイル**  
使用されません。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
場合**pDlgPage**で[ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211) CPSUI が指定したページを識別する場合、または**DlgTemplateID**で[ **DLGPAGE** ](https://msdn.microsoft.com/library/windows/hardware/ff547607) CPSUI が指定したテンプレートでは、識別**BegCtrlID**は使用されません。

それ以外の場合、 **BegCtrlID**順番に番号付きの一連のコントロール id の最初のコントロールの識別子を含める必要があります。 コントロールの id は、次の Windows コントロールを識別する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コントロールの識別子</th>
<th>Windows コントロール</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容</p></td>
<td><p>グループ ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容は + 1</p></td>
<td><p>タイトルのテキスト</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 2</p></td>
<td><p>スクロール バー</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>スクロール バーのアイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容は + 4</p></td>
<td><p>スクロール バーの範囲の下限を説明するテキスト</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>スクロール バーの範囲の上限を説明するテキスト</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>スクロール バーの単位を説明するテキスト</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 7</p></td>
<td><p>チェック ボックスを拡張または拡張のプッシュ ボタン (省略可能)</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 8</p></td>
<td><p>チェック ボックスを拡張または拡張ボタンのアイコン (省略可能)</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。 [Customizing CPSUI-Supported ウィンドウ コントロール](https://msdn.microsoft.com/library/windows/hardware/ff547296)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Compstui.h (include Compstui.h)</td>
</tr>
</tbody>
</table>

 

 




