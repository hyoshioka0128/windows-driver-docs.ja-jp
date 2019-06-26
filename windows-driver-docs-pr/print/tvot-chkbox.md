---
title: TVOT\_CHKBOX
description: TVOT\_CHKBOX
ms.assetid: 66e9879e-c101-4367-b1ee-0746e6a71bc3
keywords:
- TVOT_CHKBOX 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_CHKBOX
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec26a3c992c97849b5682f82fd4177437a3f497
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362793"
---
# <a name="tvotchkbox"></a>TVOT\_CHKBOX


## <span id="ddk_tvot_chkbox_gg"></span><span id="DDK_TVOT_CHKBOX_GG"></span>


TVOT\_CHKBOX オプションの種類は、グループ ボックス内のチェック ボックスで構成されています。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)構造体  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
使用されていません。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM$** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)構造体の配列 (**pOptParam**のメンバー [ **OPTTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
使用されていません。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
チェック ボックスに関連付けるアイコンを識別します。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
使用されていません。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)構造体  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**型**  
TVOT\_CHKBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**カウント**  
1

<span id="Style__________"></span><span id="style__________"></span><span id="STYLE__________"></span>**スタイル**   
使用されていません。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
場合**pDlgPage**で[ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui) CPSUI が指定したページを識別する場合、または**DlgTemplateID**で[ **DLGPAGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage) CPSUI が指定したテンプレートでは、識別**BegCtrlID**は使用されません。

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
<td><p>チェック ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>チェック ボックス アイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容は + 4</p></td>
<td><p>チェック ボックスを拡張または拡張のプッシュ ボタン (省略可能)</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>チェック ボックスを拡張または拡張ボタンのアイコン (省略可能)</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。 [Customizing CPSUI-Supported ウィンドウ コントロール](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)します。

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

 

 




