---
title: OID_WDI_SET_ENCAPSULATION_OFFLOAD
description: OID_WDI_SET_ENCAPSULATION_OFFLOAD は、下位の edge ドライバー (LE) が TCP チェックサム/LSO の負荷を軽減する作業を開始する必要があることを示すために OS によって送信されます。
ms.assetid: 1095DBE0-2C6B-40F4-8E01-39F4BBA2FDBC
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ENCAPSULATION_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c3bf12d25f2862372127cd8e3d2316e948d64a20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354497"
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
| [**WDI\_TLV\_設定\_カプセル化\_オフロード\_V4\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-encapsulation-offload-v4-parameters) |                                |          | IPv4 のオフロードを開始する必要があるかどうかを指定します。 |
| [**WDI\_TLV\_設定\_カプセル化\_オフロード\_V6\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-encapsulation-offload-v6-parameters) |                                |          | IPv6 のオフロードを開始する必要があるかどうかを指定します。 |

 

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

 

 




