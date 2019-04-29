---
title: OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD
description: 1 つまたは複数のプロトコルの一覧の電源管理の負荷を軽減 OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD を追加します。
ms.assetid: 50c69dd4-352d-484f-81c1-a4c9587ab368
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1fd1db45482274a5c30993f4e4dd7900e42770d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331226"
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
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP**](https://msdn.microsoft.com/library/windows/hardware/dn898035)                |                                | x        | IPv4 ARP プロトコルでは、パラメーターをオフロードします。  |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS**](https://msdn.microsoft.com/library/windows/hardware/dn898036)                  |                                | x        | IPv6 NS プロトコルでは、パラメーターをオフロードします。   |
| [**WDI\_TLV\_PM\_プロトコル\_オフロード\_80211RSN\_キー更新**](https://msdn.microsoft.com/library/windows/hardware/dn898033) |                                | x        | キーを再入力 RSN プロトコルでは、パラメーターをオフロードします。 |

 

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

 

 




