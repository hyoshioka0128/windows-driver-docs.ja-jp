---
title: TVOT\_COMBOBOX
description: TVOT\_COMBOBOX
ms.assetid: 186acda6-f87c-4e0f-95b8-d76823354cfd
keywords:
- TVOT_COMBOBOX 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_COMBOBOX
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfb6caebe89735240e3ebef141678c5a10a152d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845255"
---
# <a name="tvot_combobox"></a>TVOT\_COMBOBOX


## <span id="ddk_tvot_combobox_gg"></span><span id="DDK_TVOT_COMBOBOX_GG"></span>


TVOT\_COMBOBOX オプションの種類は、グループボックス内のコンボボックスで構成されます。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)データ  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
オプションの[**Optparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)構造体の**poptparam**メンバーによってポイントされている[**optparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)配列にインデックスを作成します。 現在選択されているオプションパラメーターを指定します。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**Optparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)構造体配列 ( [**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)の**poptparam**メンバー)  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**Poptparam**\[0\] **-&gt;、** コンボボックスに表示される最初のテキスト文字列をポイントします。

**Poptparam**\[1\]-&gt;**pData**は、コンボボックスに表示される2番目のテキスト文字列をポイントします。

**Poptparam**\[*n*\]-&gt;**pData**は、コンボボックスに表示される*n*番目のテキスト文字列をポイントします。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**Poptparam**\[0\]-&gt;**IconID**は、最初のテキスト文字列に関連付けられるアイコンを識別します。

**Poptparam**\[1\]-&gt;**IconID**は、2番目のテキスト文字列に関連付けられるアイコンを識別します。

**Poptparam**\[*n*\]-&gt;**IconID**は、 *n*番目のテキスト文字列に関連付けられるアイコンを識別します。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
使用しません。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)データ  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**各種**  
TVOT\_COMBOBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**数**  
OPTPARAM 構造体の数。これは、コンボボックスに表示されるテキスト文字列の数です。

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**スタイル**  
次のオプションのビットフラグを指定できます。

<span id="OTS_LBCB_INCL_ITEM_NONE"></span><span id="ots_lbcb_incl_item_none"></span>OTS\_LBCB\_\_項目を含む)\_なし  
設定した場合、CPSUI には、コンボボックスに "None" という文字列が含まれます。 ユーザーが [なし] を選択した場合、 **sel/psel**共用体は負の値に設定されます。

<span id="OTS_LBCB_NO_ICON16_IN_ITEM"></span><span id="ots_lbcb_no_icon16_in_item"></span>OTS\_LBCB\_\_項目に\_ICON16\_がありません  
設定した場合、CPSUI は、コンボボックスにパラメーターの値を表示するときに、各オプションパラメーターのアイコン (OPTPARAM では**IconID** ) を描画しません。

<span id="OTS_LBCB_PROPPAGE_CBUSELB"></span><span id="ots_lbcb_proppage_cbuselb"></span>OTS\_LBCB\_プロパティページ\_CBUSELB  
非ツリープロパティシートページにオプションを表示すると、コンボボックスではなく listbox として表示されます。

<span id="OTS_LBCB_SORT"></span><span id="ots_lbcb_sort"></span>OTS\_LBCB\_並べ替え  
設定すると、CPSUI はテキスト文字列をアルファベット順に表示します。

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
<td><p>コンボ ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 3</p></td>
<td><p>コンボボックスアイコン</p></td>
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

 

 




