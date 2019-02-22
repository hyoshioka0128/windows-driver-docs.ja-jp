---
title: WDI_TLV_ENABLE_WAKE_EVENTS
description: WDI_TLV_ENABLE_WAKE_EVENTS では、有効になっているウェイク イベントを含む TLV です。
ms.assetid: 5F348D9A-5575-46EE-A524-687E9D030754
ms.date: 07/18/2017
keywords:
- WDI_TLV_ENABLE_WAKE_EVENTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 749d4dd22b9446b23dd8674d9f33f56eb4224492
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553245"
---
# <a name="wditlvenablewakeevents"></a>WDI\_TLV\_を有効にする\_WAKE\_イベント


WDI\_TLV\_を有効にする\_WAKE\_イベントが有効になっているウェイク イベントを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x60 です。

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                                          |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 記載されているフラグを使用して有効になっている wake on LAN パケットのパターンを指定します[ **NDIS\_PM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566759)します。EnabledWoLPacketPatterns します。 |
| UINT32 | 有効なプロトコルの負荷を軽減に記載されているフラグを使用して指定[ **NDIS\_PM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566759)します。EnabledProtocolOffloads します。            |
| UINT32 | 記載されているフラグを使用してウェイク アップのフラグを指定[ **NDIS\_PM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566759)します。WakeUpFlags します。                                    |
| UINT32 | メディアに固有の復帰に記載されているフラグを使用してイベントを指定します[ **NDIS\_PM\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566759)します。MediaSpecificWakeUpEvents します。      |

 

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

 

 




