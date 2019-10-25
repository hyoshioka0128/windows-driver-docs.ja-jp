---
title: IWiaDrvItem COM インターフェイス
description: IWiaDrvItem COM インターフェイス
ms.assetid: 1be2265b-7ae8-4935-9559-588b885526d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7b27b9526c13ef373f71b121a6cf5bef286476
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840801"
---
# <a name="iwiadrvitem-com-interface"></a>IWiaDrvItem COM インターフェイス





[IWiaDrvItem インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)には、WIA ミニドライバーが**IWiaDrvItem**項目のツリーを管理するために使用するメソッドが用意されています。 これらのメソッドは、WIA ミニドライバーが**IWiaDrvItem**オブジェクトを操作できるようにします。 **IWiaDrvItem**インターフェイスには、次のメソッドが用意されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder" data-raw-source="[&lt;strong&gt;IWiaDrvItem::AddItemToFolder&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)"><strong>IWiaDrvItem:: AddItemToFolder</strong></a></p></td>
<td><p><strong>IWiaDrvItem</strong>オブジェクトをフォルダーに追加します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-dumpitemdata" data-raw-source="[&lt;strong&gt;IWiaDrvItem::DumpItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-dumpitemdata)"><strong>IWiaDrvItem::D umpItemData</strong></a></p></td>
<td><p>プライベートドライバー項目データをダンプします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-findchilditembyname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindChildItemByName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-findchilditembyname)"><strong>IWiaDrvItem::FindChildItemByName</strong></a></p></td>
<td><p>項目の完全な名前で子項目を検索します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-finditembyname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindItemByName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-finditembyname)"><strong>IWiaDrvItem::FindItemByName</strong></a></p></td>
<td><p>項目の完全な名前で項目を検索します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getdevicespeccontext" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetDeviceSpecContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getdevicespeccontext)"><strong>IWiaDrvItem::GetDeviceSpecContext</strong></a></p></td>
<td><p>デバイス固有のコンテキストへのポインターを取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFirstChildItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfirstchilditem)"><strong>IWiaDrvItem::GetFirstChildItem</strong></a></p></td>
<td><p>このフォルダー項目の最初の子を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfullitemname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFullItemName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getfullitemname)"><strong>IWiaDrvItem::GetFullItemName</strong></a></p></td>
<td><p>項目の完全な名前と階層情報を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemFlags&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemflags)"><strong>IWiaDrvItem::GetItemFlags</strong></a></p></td>
<td><p>WIA 項目フラグを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemname" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getitemname)"><strong>IWiaDrvItem::GetItemName</strong></a></p></td>
<td><p>項目名を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetNextSiblingItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getnextsiblingitem)"><strong>IWiaDrvItem::GetNextSiblingItem</strong></a></p></td>
<td><p>この項目の次の兄弟を検索します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetParentItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-getparentitem)"><strong>IWiaDrvItem::GetParentItem</strong></a></p></td>
<td><p>この項目の親項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-removeitemfromfolder" data-raw-source="[&lt;strong&gt;IWiaDrvItem::RemoveItemFromFolder&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-removeitemfromfolder)"><strong>IWiaDrvItem:: RemoveItemFromFolder</strong></a></p></td>
<td><p>親フォルダーから項目を削除します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-unlinkitemtree" data-raw-source="[&lt;strong&gt;IWiaDrvItem::UnlinkItemTree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-unlinkitemtree)"><strong>IWiaDrvItem:: UnlinkItemTree</strong></a></p></td>
<td><p>ドライバー項目ツリーのリンクを解除します。</p></td>
</tr>
</tbody>
</table>

 

 

 




