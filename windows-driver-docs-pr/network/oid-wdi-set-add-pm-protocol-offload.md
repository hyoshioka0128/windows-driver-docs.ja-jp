---
title: OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD
description: 1 つまたは複数のプロトコルの一覧の電源管理の負荷を軽減 OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD を追加します。
ms.assetid: 50c69dd4-352d-484f-81c1-a4c9587ab368
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cd47b8cd9f4fc80ae2c6bea40ac4778223b8d08e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387260"
---
# <a name="oidwdisetaddpmprotocoloffload"></a>OID\_WDI\_設定\_追加\_PM\_プロトコル\_オフロード


OID\_WDI\_設定\_追加\_PM\_プロトコル\_オフロードが 1 つまたは複数のプロトコルの一覧の電源管理の負荷を軽減を追加します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

このプロパティは、メインの CPU がスリープ状態中に、これらのプロトコルを実装するためにデバイスまたはファームウェアを有効にする情報を提供します。 この状態で、ファームウェア、およびデバイスは、ホストを起動せず、オフロードされたタスクを処理します。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-ipv4arp)                |                                | x        | IPv4 ARP プロトコルでは、パラメーターをオフロードします。  |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-ipv6ns)                  |                                | x        | IPv6 NS プロトコルでは、パラメーターをオフロードします。   |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_80211RSN\_キー更新**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-protocol-offload-80211rsn-rekey) |                                | x        | キーを再入力 RSN プロトコルでは、パラメーターをオフロードします。 |

 

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


[OID\_WDI\_取得\_PM\_プロトコル\_オフロード](oid-wdi-get-pm-protocol-offload.md)

[OID\_WDI\_設定\_削除\_PM\_プロトコル\_オフロード](oid-wdi-set-remove-pm-protocol-offload.md)

 

 




