---
title: OID_WDI_GET_PM_PROTOCOL_OFFLOAD
description: OID_WDI_GET_PM_PROTOCOL_OFFLOAD 要求、プロトコルの一覧の電源管理の負荷を軽減します。
ms.assetid: ed7604fa-666c-4aa1-9041-ed56d282c29b
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_PM_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: af84ff750e1351dd3c5973ccb143ef0a8a3edfcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353675"
---
# <a name="oidwdigetpmprotocoloffload"></a>OID\_WDI\_取得\_PM\_プロトコル\_オフロード


OID\_WDI\_取得\_PM\_プロトコル\_オフロード要求プロトコルの一覧の電源管理の負荷を軽減します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 該当なし           | 1                               |

 

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


| TLV                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明          |
|--------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_取得**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-get) |                                |          | プロトコルのオフロードの id。 |

 

## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-ipv4arp)                |                                | x        | IPv4 ARP プロトコルでは、パラメーターをオフロードします。  |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-ipv6ns)                  |                                | x        | IPv6 NS プロトコルでは、パラメーターをオフロードします。   |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_80211RSN\_キー更新**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-80211rsn-rekey) |                                | x        | キーを再入力 RSN プロトコルでは、パラメーターをオフロードします。 |

 

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


[OID\_WDI\_設定\_追加\_PM\_プロトコル\_オフロード](oid-wdi-set-add-pm-protocol-offload.md)

[OID\_WDI\_設定\_削除\_PM\_プロトコル\_オフロード](oid-wdi-set-remove-pm-protocol-offload.md)

 

 




