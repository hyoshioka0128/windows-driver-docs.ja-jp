---
title: WDI_TLV_ENABLE_WAKE_EVENTS
description: WDI_TLV_ENABLE_WAKE_EVENTS は、有効なウェイクイベントを含む TLV です。
ms.assetid: 5F348D9A-5575-46EE-A524-687E9D030754
ms.date: 07/18/2017
keywords:
- WDI_TLV_ENABLE_WAKE_EVENTS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: bedd644ca8db67bdb6d1a530a4dfb46d9a83db04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834101"
---
# <a name="wdi_tlv_enable_wake_events"></a>WDI\_TLV\_\_ウェイク\_イベントを有効にする


WDI\_TLV\_ENABLE\_WAKE\_EVENTS は、有効なウェイクイベントを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x60

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                                                                                          |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)に記載されているフラグを使用して、有効な WAKE on LAN パケットパターンを指定します。EnabledWoLPacketPatterns. |
| UINT32 | [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)に記載されているフラグを使用して、有効なプロトコルオフロードを指定します。EnabledProtocolOffloads.            |
| UINT32 | [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)に記載されているフラグを使用して、ウェイクアップフラグを指定します。WakeUpFlags.                                    |
| UINT32 | [**NDIS\_PM\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)に記載されているフラグを使用して、メディア固有のウェイクアップイベントを指定します。MediaSpecificWakeUpEvents.      |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




