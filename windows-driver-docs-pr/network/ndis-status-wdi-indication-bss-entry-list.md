---
title: NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST を使用して、BSS エントリの更新について、ホストに通知します。 これにより、要請していないことを示しています、いつでも送信できます。
ms.assetid: 5b9fd7b1-0817-4b86-9acc-b4f99cb7ae9a
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_BSS_ENTRY_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 64b9baa9f923b3b4b8064f8ddc28342088736e1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366401"
---
# <a name="ndisstatuswdiindicationbssentrylist"></a>NDIS\_状態\_WDI\_INDICATION\_BSS\_エントリ\_一覧


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_BSS\_エントリ\_BSS エントリの更新について、ホストに通知を一覧します。 これにより、要請していないことを示しています、いつでも送信できます。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                 |
|--------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_BSS\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn926162) | x                              | x        | 更新された Bssid の一覧。 |

 

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


[OID\_WDI\_タスク\_スキャン](oid-wdi-task-scan.md)

[OID\_WDI\_タスク\_P2P\_検出](oid-wdi-task-p2p-discover.md)

[OID\_WDI\_設定\_P2P\_開始\_バック グラウンド\_検出](oid-wdi-set-p2p-start-background-discovery.md)

 

 




