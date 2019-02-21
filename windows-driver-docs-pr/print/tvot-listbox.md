---
title: TVOT\_LISTBOX
description: TVOT\_LISTBOX
ms.assetid: 2426ae5a-33e6-4f16-ad49-ff38ea19e392
keywords:
- TVOT_LISTBOX 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_LISTBOX
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d232a061d729fd52d781e5357f9a846ef3beba3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551876"
---
# <a name="tvotlistbox"></a>TVOT\_LISTBOX


## <span id="ddk_tvot_listbox_gg"></span><span id="DDK_TVOT_LISTBOX_GG"></span>


TVOT\_LISTBOX オプションの種類は、グループ ボックス内でリスト ボックスで構成されています。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
内のインデックス、 [ **OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)が指す配列、 **pOptParam**のオプションのメンバー [ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体。 これには、現在選択されているオプションのパラメーターを指定します。

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)構造体の配列 (**pOptParam**のメンバー [ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
**pOptParam**\[0\]-&gt;**pData**リスト ボックスに表示される最初のテキスト文字列を指します。

**pOptParam**\[1\]-&gt;**pData**リスト ボックスに表示される 2 つ目のテキスト文字列を指します。

**pOptParam**\[*n*\]-&gt;**pData**を指す、 *n*番目の文字列を表示するにはリスト ボックス。

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
**pOptParam**\[0\]-&gt;**IconID**に文字列が最初に関連付けるアイコンを識別します。

**pOptParam**\[1\]-&gt;**IconID**に 2 つ目のテキスト文字列に関連付けるアイコンを識別します。

**pOptParam**\[*n*\]-&gt;**IconID**に関連付けるアイコンを識別、 *n*番目のテキスト文字列。

<span id="lParam"></span><span id="lparam"></span><span id="LPARAM"></span>**lParam**  
使用されません。

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体  

<span id="Type"></span><span id="type"></span><span id="TYPE"></span>**型**  
TVOT\_LISTBOX

<span id="Count"></span><span id="count"></span><span id="COUNT"></span>**カウント**  
OPTPARAM$ の構造体の数つまり、テキストの数は、リスト ボックスに表示される文字列です。

<span id="Style"></span><span id="style"></span><span id="STYLE"></span>**スタイル**  
次のオプションのビット フラグを指定することができます。

<span id="OTS_LBCB_INCL_ITEM_NONE"></span><span id="ots_lbcb_incl_item_none"></span>OTS\_LBCB\_含める\_項目\_NONE  
設定すると、CPSUI が含まれるかどうか"None"、リスト ボックス内の文字列。 "None"を選択した場合、 **Sel/pSel**共用体は、負の 1 に設定されます。

<span id="OTS_LBCB_NO_ICON16_IN_ITEM"></span><span id="ots_lbcb_no_icon16_in_item"></span>OTS\_LBCB\_いいえ\_ICON16\_IN\_項目  
かどうか設定、CPSUI 描画されません。 各オプションのパラメーターのアイコン (**IconID** OPTPARAM$ で)、リスト ボックスで、パラメーターの値を表示するときにします。

<span id="OTS_LBCB_PROPPAGE_LBUSECB"></span><span id="ots_lbcb_proppage_lbusecb"></span>OTS\_LBCB\_プロパティ ページ\_LBUSECB  
Nontreeview プロパティ シート ページのオプションが表示されたら、リスト ボックスではなくコンボ ボックスとして表示されます。

<span id="OTS_LBCB_SORT"></span><span id="ots_lbcb_sort"></span>OTS\_LBCB\_並べ替え  
CPSUI セットには、アルファベット順でのテキスト文字列が表示されます。 場合、

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
<td><p>リスト ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>リスト ボックスのアイコン</p></td>
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

 

 




