---
title: OID_WDI_SET_ENCAPSULATION_OFFLOAD
description: OID_WDI_SET_ENCAPSULATION_OFFLOAD は、下位の edge ドライバー (LE) が TCP チェックサム/LSO の負荷を軽減する作業を開始する必要があることを示すために OS によって送信されます。
ms.assetid: 1095DBE0-2C6B-40F4-8E01-39F4BBA2FDBC
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ENCAPSULATION_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 38e437abee229a0e40067e94a8111eb3261a4708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330176"
---
# <a name="oidwdisetencapsulationoffload"></a>OID\_WDI\_設定\_カプセル化\_オフロード


OID\_WDI\_設定\_カプセル化\_LSO/TCP チェックサム オフロードを実行する下位の edge ドライバー (LE) が開始されるかを示す、OS から送信されるオフロードします。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

このメッセージが受信したときに、LE がでの現在のカプセル化オフロードの構成を示す必要があります[NDIS\_状態\_WDI\_INDICATION\_タスク\_オフロード\_現在\_CONFIG](ndis-status-wdi-indication-task-offload-current-config.md)します。 受信操作の場合は、LE する必要があります、OID を受け取った後までチェックサム オフロード起動しない\_WDI\_設定\_カプセル化\_オフロード メッセージ。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                     |
|-----------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_設定\_カプセル化\_オフロード\_V4\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898058) |                                |          | IPv4 のオフロードを開始する必要があるかどうかを指定します。 |
| [**WDI\_TLV\_設定\_カプセル化\_オフロード\_V6\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898059) |                                |          | IPv6 のオフロードを開始する必要があるかどうかを指定します。 |

 

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

 

 




