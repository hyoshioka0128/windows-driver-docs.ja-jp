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
ms.openlocfilehash: 6335ca9337cf1d39f19cfd62bd12ce3f5927b05a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845257"
---
# <a name="tvot_chkbox"></a>TVOT\_CHKBOX


## <span id="ddk_tvot_chkbox_gg"></span><span id="DDK_TVOT_CHKBOX_GG"></span>


TVOT\_CHKBOX オプションの種類は、グループボックス内のチェックボックスで構成されます。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)データ  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
使用しません。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**Optparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)構造体配列 ( [**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)の**poptparam**メンバー)  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
使用しません。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
チェックボックスに関連付けられるアイコンを識別します。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
使用しません。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)データ  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**各種**  
TVOT\_CHKBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**数**  
1

<span id="Style__________"></span><span id="style__________"></span><span id="STYLE__________"></span>**スタイル**   
使用しません。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)の**pDlgPage**が CPSUI 提供のページを識別する場合、または[**DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)の**DlgTemplateID**が CPSUI で提供されるテンプレートを識別する場合、 **begctrlid**は使用されません。

それ以外の場合、 **Begctrlid**には、順番に番号が付けられた一連のコントロール id の最初のコントロール識別子が含まれている必要があります。 コントロール識別子は、次の Windows コントロールを識別する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コントロール識別子</th>
<th>Windows コントロール</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Begctrlid</strong>の内容</p></td>
<td><p>グループボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 1</p></td>
<td><p>タイトルのテキスト</p></td>
</tr>
<tr class="odd">
<td><p><strong>Begctrlid</strong>コンテンツ + 2</p></td>
<td><p>チェック ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 3</p></td>
<td><p>チェックボックスアイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>Begctrlid</strong>コンテンツ + 4</p></td>
<td><p>拡張チェックボックスまたは拡張プッシュボタン (オプション)</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 5</p></td>
<td><p>拡張チェックボックスまたは拡張プッシュボタンアイコン (省略可能)</p></td>
</tr>
</tbody>
</table>

 

詳細については、「 [CPSUI でサポートされているウィンドウコントロールのカスタマイズ](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)」を参照してください。

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
<td>Compstui (Compstui を含む)</td>
</tr>
</tbody>
</table>

 

 




