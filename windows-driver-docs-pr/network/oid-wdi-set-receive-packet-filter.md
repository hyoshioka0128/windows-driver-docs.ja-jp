---
title: OID_WDI_SET_RECEIVE_PACKET_FILTER
description: OID_WDI_SET_RECEIVE_PACKET_FILTER は、特定の仮想化されたポートを示すデータ パケットのビットマスクのフィルターを定義します。
ms.assetid: 180efda5-3ca2-40f8-89d1-098a53f33844
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_RECEIVE_PACKET_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 71174eab83b2c0593cbd49dc2bf81b62731a6a6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359181"
---
# <a name="oidwdisetreceivepacketfilter"></a>OID\_WDI\_設定\_受信\_パケット\_フィルター


OID\_WDI\_設定\_受信\_パケット\_フィルターは、特定の仮想化されたポートを示すデータ パケットのビットマスクのフィルターを定義します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

かどうか設定すると、ポートは通知のみ指定されたフィルターに一致するパケットのホスト。 これらのフィルターに必要な 802.11 フィルターと同様に[OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)します。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                          |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI\_TLV\_パケット\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-packet-filter-parameters) |                                |          | データ パケットのビットマスク フィルターです。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

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

 

 




