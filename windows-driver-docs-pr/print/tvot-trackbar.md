---
title: TVOT\_トラック バー
description: TVOT\_トラック バー
ms.assetid: 00140dca-c192-42dc-853d-ae84c602b206
keywords:
- TVOT_TRACKBAR 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_TRACKBAR
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39639b7b2bfe08b1b804877758f0e8b51c891d1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390246"
---
# <a name="tvottrackbar"></a>TVOT\_トラック バー


## <span id="ddk_tvot_trackbar_gg"></span><span id="DDK_TVOT_TRACKBAR_GG"></span>


TVOT\_グループ ボックス内のトラック バーのトラック バー オプションの種類で構成されます。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
現在のトラック バーの位置を表す値。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)構造体の配列 (**pOptParam**のメンバー [ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**トラック バーの単位を識別するテキストの NULL で終わる文字列を指します。

**pOptParam**\[1\]-&gt;**pData**トラック バーの範囲の下限を説明するテキストの NULL で終わる文字列を指します。

**pOptParam**\[2\]-&gt;**pData**トラック バーの範囲の上限を説明するテキストの NULL で終わる文字列を指します。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**トラック バーに関連付けるアイコンを識別します。

**pOptParam**\[1\]-&gt;**IconID**トラック バーの範囲の下限を表す 16 ビット符号付きの値を指定します。

**pOptParam**\[2\]-&gt;**IconID**その値が表示される選択された追跡位置 gefore に適用される乗算の係数を指定します。 (通常は、この値は 1 です。)

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
**pOptParam**\[0\]-&gt;**lParam**は使用されません。

**pOptParam**\[1\]-&gt;**lParam**トラック バーの範囲の上限を表す 16 ビット符号付きの値を指定します。

**pOptParam**\[2\]-&gt;**lParam**追跡を指定する値をインクリメントします。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**型**  
TVOT\_トラック バー

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**カウント**  
3

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**スタイル**  
使用されていません。

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
<td><p>トラック バー</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>トラック バーのアイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容は + 4</p></td>
<td><p>トラック バーの範囲の下限を説明するテキスト</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>トラック バーの範囲の上限を説明するテキスト</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>トラック バーの単位を説明するテキスト</p></td>
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

<a name="requirements"></a>要件
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

 

 




