---
title: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS
description: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS に送信されます、デバイス、OS から TCP オフロード パラメーターを設定します。
ms.assetid: B615066B-3871-4445-8397-B41CB66EEF35
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_TCP_OFFLOAD_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f5291629c4436bc405a9ae9cfaba4ea1d1274b3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386529"
---
# <a name="oidwdisettcpoffloadparameters"></a>OID\_WDI\_設定\_TCP\_オフロード\_パラメーター


OID\_WDI\_設定\_TCP\_オフロード\_パラメーターからに送信されたデバイスを設定する OS TCP オフロード パラメーター。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

このコマンドが送信される場合などによって必要があるパフォーマンスの問題のためのオフロードを無効にします。

下位の edge ドライバー (LE) の内容を使用する必要があります[ **WDI\_TLV\_TCP\_設定\_オフロード\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-set-offload-parameters)を更新する、現在 TCP オフロード機能を報告します。 LE、更新した後では、現在のタスク オフロード機能を報告する必要があります[NDIS\_状態\_WDI\_INDICATION\_タスク\_オフロード\_現在\_CONFIG](ndis-status-wdi-indication-task-offload-current-config.md)します。 この状態を示す値により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                           |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI\_TLV\_TCP\_設定\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-set-offload-parameters) |                                |          | TCP では、パラメーターを設定できるをオフロードします。 |

 

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

 

 




