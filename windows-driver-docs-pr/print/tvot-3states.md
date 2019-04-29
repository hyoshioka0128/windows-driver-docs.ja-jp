---
title: TVOT\_3STATES
description: TVOT\_3STATES
ms.assetid: baa9fa5e-521e-446b-bd6c-7910d61c7764
keywords:
- TVOT_3STATES 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_3STATES
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f9e9506eaa0d0f7bcb66f5250303ae24a8c6493
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326025"
---
# <a name="tvot3states"></a>TVOT\_3STATES


## <span id="ddk_tvot_3states_gg"></span><span id="DDK_TVOT_3STATES_GG"></span>


TVOT\_3STATES オプションの種類は、グループ ボックス内の 3 つのラジオ ボタンで構成されています。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
内のインデックス、 [ **OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)が指す配列、 **pOptParam**のオプションのメンバー [ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体。 これには、現在選択されているオプションのパラメーターを指定します。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)構造体の配列 (**pOptParam**のメンバー [ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**状態 1、ボタンのラベルとして使用されるを記述するテキスト文字列を指します。

**pOptParam**\[1\]-&gt;**pData**状態 2、ボタンのラベルとして使用されるを記述するテキスト文字列を指します。

**pOptParam**\[2\]-&gt;**pData**状態 3、ボタンのラベルとして使用されるを記述するテキスト文字列を指します。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**状態 1 に関連付けるアイコンを識別します。

**pOptParam**\[1\]-&gt;**IconID**状態 2 に関連付けるアイコンを識別します。

**pOptParam**\[2\]-&gt;**IconID**状態 3 に関連付けるアイコンを識別します。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
使用されていません。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**型**  
TVOT\_3STATES

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
<td><p>状態 1 のラジオ ボタン</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>状態 1 アイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容は + 4</p></td>
<td><p>State 2 ラジオ ボタン</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>State 2 アイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 6</p></td>
<td><p>状態 3 のオプション ボタン</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 7</p></td>
<td><p>状態 3 アイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 8</p></td>
<td><p>チェック ボックスを拡張または拡張のプッシュ ボタン (省略可能)</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 9</p></td>
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

 

 




