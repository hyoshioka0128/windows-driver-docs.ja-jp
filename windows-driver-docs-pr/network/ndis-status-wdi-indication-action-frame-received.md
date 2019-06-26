---
title: NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED を使用して、操作、フレームが受信されたことを示します。
ms.assetid: C1F6EB50-C11F-428F-BF51-5C89A59CBF76
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 436a98f43fbb5e91aa736d5ff3b490cb8704aa04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382203"
---
# <a name="ndisstatuswdiindicationactionframereceived"></a>NDIS\_状態\_WDI\_INDICATION\_アクション\_フレーム\_受信日時


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_アクション\_フレーム\_を操作するフレームが受信されたことを示すために受信します。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                               |
|------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)                                      |                                |          | ソースの BSSID します。                                  |
| [**WDI\_TLV\_BSS\_エントリ\_チャネル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry-channel-info) |                                |          | BSS エントリに論理チャネル数と帯域 ID。 |
| [**WDI\_TLV\_アクション\_フレーム\_本文**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-action-frame-body)            |                                |          | 受信操作フレーム本体。                           |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_広告\_情報](oid-wdi-set-advertisement-information.md)

 

 




