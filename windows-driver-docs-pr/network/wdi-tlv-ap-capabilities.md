---
title: WDI_TLV_AP_CAPABILITIES
description: WDI_TLV_AP_CAPABILITIES では、アクセス ポイントの機能を含む TLV です。
ms.assetid: 2DE866C8-9414-46D8-A156-3A35F1E325EF
ms.date: 07/18/2017
keywords:
- WDI_TLV_AP_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b3d2f981feba63dd6f43a012e9719e16920bc0c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362844"
---
# <a name="wditlvapcapabilities"></a>WDI\_TLV\_AP\_機能


WDI\_TLV\_AP\_機能は、アクセス ポイントの機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x16

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
<td>UINT32</td>
<td>スキャン SSID リストのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>必要な SSID リストのサイズ。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>プライバシーの除外リストのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>関連テーブルのサイズ。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>キー マップ テーブルのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>既定のテーブルのキー サイズ。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>WEP キー値の最大長。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>AP がレーダーの検出をサポートしているかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
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

 

 




