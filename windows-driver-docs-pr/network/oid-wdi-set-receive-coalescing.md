---
title: OID_WDI_SET_RECEIVE_COALESCING
description: OID_WDI_SET_RECEIVE_COALESCING は、パケットの結合のパケット フィルターを追加する、ホストによって使用されます。
ms.assetid: c8856813-0d81-4735-95cc-d9b5dc6ede87
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_RECEIVE_COALESCING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 031fb37ae82bf68d4149c89839d1951c5c1a2d9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359169"
---
# <a name="oidwdisetreceivecoalescing"></a>OID\_WDI\_設定\_受信\_COALESCING


OID\_WDI\_設定\_受信\_COALESCING がパケットの結合のパケット フィルターを追加する、ホストによって使用されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

ホストは、パケットの結合フィルターの設定を OS からの要求を受信したときに、パケットの結合のパケット フィルターを追加するのにこのコマンドを使用します。 パケットの結合のパケット フィルターをクリアするを参照してください。 [OID\_WDI\_設定\_オフ\_受信\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)します。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                 |
|-----------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**WDI\_TLV\_設定\_受信\_COALESCING**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-receive-coalescing) |                                |          | 設定するパケット結合パラメーター。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加のパラメーターはありません。 ヘッダー内のデータで十分です。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_クリア\_受信\_COALESCING](oid-wdi-set-clear-receive-coalescing.md)

 

 




