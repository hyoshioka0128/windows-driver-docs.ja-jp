---
title: WDI_TLV_BSS_ENTRY_AGE_INFO
description: WDI_TLV_BSS_ENTRY_AGE_INFO は、BSS エントリの有効期間情報を含む TLV です。
ms.assetid: 3D0DC599-2A66-45E9-B02C-32291A028139
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_ENTRY_AGE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b89ffc3be66d87efc8ed80ecdf8d8a03eb127b87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327570"
---
# <a name="wditlvbssentryageinfo"></a>WDI\_TLV\_BSS\_エントリ\_年齢\_情報


WDI\_TLV\_BSS\_エントリ\_年齢\_情報が BSS エントリの有効期間情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xBA

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT64</td>
<td>この BSS エントリが最後に検出されたときのタイムスタンプ。 タイムスタンプを取得する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff562629" data-raw-source="[&lt;strong&gt;NdisGetCurrentSystemTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562629)"> <strong>NdisGetCurrentSystemTime</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff553068" data-raw-source="[&lt;strong&gt;KeQuerySystemTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553068)"> <strong>KeQuerySystemTime</strong></a>します。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>かどうかについてはこのライブ (現在実行中のスキャン中に見つかった) を指定します。 または、IHV コンポーネントの BSS リストのキャッシュに由来します。
<p>有効な値は 0 (live) または 1 (キャッシュ)。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




