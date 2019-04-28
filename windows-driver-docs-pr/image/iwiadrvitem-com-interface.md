---
title: IWiaDrvItem COM インターフェイス
description: IWiaDrvItem COM インターフェイス
ms.assetid: 1be2265b-7ae8-4935-9559-588b885526d4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd3ae78f0c84269c5743fba8443d4e6811f22746
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381814"
---
# <a name="iwiadrvitem-com-interface"></a>IWiaDrvItem COM インターフェイス





[IWiaDrvItem インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543896)WIA ミニドライバーは、ツリーの管理を使用してメソッドを提供します**IWiaDrvItem**項目。 これらのメソッドにより、WIA ミニドライバーを操作する**IWiaDrvItem**オブジェクト。 **IWiaDrvItem**インターフェイスは、次のメソッドを提供します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543856" data-raw-source="[&lt;strong&gt;IWiaDrvItem::AddItemToFolder&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543856)"><strong>IWiaDrvItem::AddItemToFolder</strong></a></p></td>
<td><p>追加、 <strong>IWiaDrvItem</strong>フォルダーへのオブジェクト。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543863" data-raw-source="[&lt;strong&gt;IWiaDrvItem::DumpItemData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543863)"><strong>IWiaDrvItem::DumpItemData</strong></a></p></td>
<td><p>プライベート ドライバー項目データをダンプします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543867" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindChildItemByName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543867)"><strong>IWiaDrvItem::FindChildItemByName</strong></a></p></td>
<td><p>完全な項目名では、子項目を検索します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543870" data-raw-source="[&lt;strong&gt;IWiaDrvItem::FindItemByName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543870)"><strong>IWiaDrvItem::FindItemByName</strong></a></p></td>
<td><p>完全な項目の名前で項目を検索します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543873" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetDeviceSpecContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543873)"><strong>IWiaDrvItem::GetDeviceSpecContext</strong></a></p></td>
<td><p>デバイス固有のコンテキストへのポインターを取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543878" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFirstChildItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543878)"><strong>IWiaDrvItem::GetFirstChildItem</strong></a></p></td>
<td><p>このフォルダーの項目の最初の子を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543881" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetFullItemName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543881)"><strong>IWiaDrvItem::GetFullItemName</strong></a></p></td>
<td><p>取得します完全な名前と階層情報の項目。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543883" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemFlags&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543883)"><strong>IWiaDrvItem::GetItemFlags</strong></a></p></td>
<td><p>WIA 項目のフラグを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543885" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetItemName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543885)"><strong>IWiaDrvItem::GetItemName</strong></a></p></td>
<td><p>項目の名前を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543889" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetNextSiblingItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543889)"><strong>IWiaDrvItem::GetNextSiblingItem</strong></a></p></td>
<td><p>この項目の次の兄弟を検索します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543892" data-raw-source="[&lt;strong&gt;IWiaDrvItem::GetParentItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543892)"><strong>IWiaDrvItem::GetParentItem</strong></a></p></td>
<td><p>この項目の親項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543899" data-raw-source="[&lt;strong&gt;IWiaDrvItem::RemoveItemFromFolder&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543899)"><strong>IWiaDrvItem::RemoveItemFromFolder</strong></a></p></td>
<td><p>親フォルダーから項目を削除します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543901" data-raw-source="[&lt;strong&gt;IWiaDrvItem::UnlinkItemTree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543901)"><strong>IWiaDrvItem::UnlinkItemTree</strong></a></p></td>
<td><p>ドライバーの項目のツリーのリンクを解除します。</p></td>
</tr>
</tbody>
</table>

 

 

 




