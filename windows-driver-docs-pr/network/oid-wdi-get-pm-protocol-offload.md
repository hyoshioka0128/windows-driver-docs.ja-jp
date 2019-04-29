---
title: OID_WDI_GET_PM_PROTOCOL_OFFLOAD
description: OID_WDI_GET_PM_PROTOCOL_OFFLOAD 要求、プロトコルの一覧の電源管理の負荷を軽減します。
ms.assetid: ed7604fa-666c-4aa1-9041-ed56d282c29b
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_PM_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bcf76fc7b72c98e94625216dcdfb2a1f5a2b43d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391967"
---
# <a name="oidwdigetpmprotocoloffload"></a>OID\_WDI\_取得\_PM\_プロトコル\_オフロード


OID\_WDI\_取得\_PM\_プロトコル\_オフロード要求プロトコルの一覧の電源管理の負荷を軽減します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 該当なし           | 1                               |

 

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


| TLV                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明          |
|--------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_取得**](https://msdn.microsoft.com/library/windows/hardware/dn898034) |                                |          | プロトコルのオフロードの id。 |

 

## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP**](https://msdn.microsoft.com/library/windows/hardware/dn898035)                |                                | x        | IPv4 ARP プロトコルでは、パラメーターをオフロードします。  |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS**](https://msdn.microsoft.com/library/windows/hardware/dn898036)                  |                                | x        | IPv6 NS プロトコルでは、パラメーターをオフロードします。   |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_80211RSN\_キー更新**](https://msdn.microsoft.com/library/windows/hardware/dn898033) |                                | x        | キーを再入力 RSN プロトコルでは、パラメーターをオフロードします。 |

 

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

 

 




