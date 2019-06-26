---
title: OID_WDI_SET_CLEAR_RECEIVE_COALESCING
description: OID_WDI_SET_CLEAR_RECEIVE_COALESCING は、パケットの結合のパケット フィルターを削除する、ホストによって使用されます。
ms.assetid: 1c2848c4-c412-4f33-9fc6-bf900a89c65d
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_CLEAR_RECEIVE_COALESCING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0e8e0196ad192f0b8ed54d33a5f985b26fe659d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387249"
---
# <a name="oidwdisetclearreceivecoalescing"></a>OID\_WDI\_設定\_クリア\_受信\_COALESCING


OID\_WDI\_設定\_クリア\_受信\_COALESCING がパケットの結合のパケット フィルターを削除する、ホストによって使用されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                            | 許可されている複数の TLV インスタンス | 省略可能 | 説明                         |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_設定\_クリア\_受信\_COALESCING**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-clear-receive-coalescing) |                                |          | 削除するパケット フィルター ID。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

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


[OID\_WDI\_設定\_受信\_COALESCING](oid-wdi-set-receive-coalescing.md)

 

 




