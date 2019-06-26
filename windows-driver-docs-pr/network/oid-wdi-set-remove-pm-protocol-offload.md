---
title: OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD
description: プロトコルで指定されたプロトコル、オフロード OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD 削除オフロード id。
ms.assetid: 47850c43-4d10-48f5-b2e9-1f94f23eabf2
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_REMOVE_PM_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0b5664b13de9c40044d71b024e80e41bc2bc53db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384205"
---
# <a name="oidwdisetremovepmprotocoloffload"></a>OID\_WDI\_設定\_削除\_PM\_プロトコル\_オフロード


OID\_WDI\_設定\_削除\_PM\_プロトコル\_プロトコルによって指定されたプロトコル、オフロード オフロード削除オフロード id。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明          |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_削除**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-remove) |                                |          | プロトコルのオフロードの id。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加のパラメーターはありません。 ヘッダー内のデータで十分です。

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


[OID\_WDI\_取得\_PM\_プロトコル\_オフロード](oid-wdi-get-pm-protocol-offload.md)

[OID\_WDI\_設定\_追加\_PM\_プロトコル\_オフロード](oid-wdi-set-add-pm-protocol-offload.md)

 

 




