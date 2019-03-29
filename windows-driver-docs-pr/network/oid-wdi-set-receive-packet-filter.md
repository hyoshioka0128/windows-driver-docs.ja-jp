---
title: OID_WDI_SET_RECEIVE_PACKET_FILTER
description: OID_WDI_SET_RECEIVE_PACKET_FILTER は、特定の仮想化されたポートを示すデータ パケットのビットマスクのフィルターを定義します。
ms.assetid: 180efda5-3ca2-40f8-89d1-098a53f33844
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_RECEIVE_PACKET_FILTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c3689ef12a32c38a5ae424b28a1d3b0357778eed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581808"
---
# <a name="oidwdisetreceivepacketfilter"></a>OID\_WDI\_設定\_受信\_パケット\_フィルター


OID\_WDI\_設定\_受信\_パケット\_フィルターは、特定の仮想化されたポートを示すデータ パケットのビットマスクのフィルターを定義します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | はい                      | 1                               |

 

かどうか設定すると、ポートは通知のみ指定されたフィルターに一致するパケットのホスト。 これらのフィルターに必要な 802.11 フィルターと同様に[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)します。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                          |
|---------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------|
| [**WDI\_TLV\_パケット\_フィルター\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898019) |                                |          | データ パケットのビットマスク フィルターです。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
必要条件
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

 

 




