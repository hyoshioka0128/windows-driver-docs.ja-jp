---
title: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS
description: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS に送信されます、デバイス、OS から TCP オフロード パラメーターを設定します。
ms.assetid: B615066B-3871-4445-8397-B41CB66EEF35
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_TCP_OFFLOAD_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 586ca294c072473e3fb62e85829e19893999f985
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348512"
---
# <a name="oidwdisettcpoffloadparameters"></a>OID\_WDI\_設定\_TCP\_オフロード\_パラメーター


OID\_WDI\_設定\_TCP\_オフロード\_パラメーターからに送信されたデバイスを設定する OS TCP オフロード パラメーター。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

このコマンドが送信される場合などによって必要があるパフォーマンスの問題のためのオフロードを無効にします。

下位の edge ドライバー (LE) の内容を使用する必要があります[ **WDI\_TLV\_TCP\_設定\_オフロード\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/dn898071)を更新する、現在 TCP オフロード機能を報告します。 LE、更新した後では、現在のタスク オフロード機能を報告する必要があります[NDIS\_状態\_WDI\_INDICATION\_タスク\_オフロード\_現在\_CONFIG](ndis-status-wdi-indication-task-offload-current-config.md)します。 この状態を示す値により、新しい機能の情報ですべての上位のプロトコルのドライバーが更新されるようになります。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                           |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI\_TLV\_TCP\_設定\_オフロード\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898071) |                                |          | TCP では、パラメーターを設定できるをオフロードします。 |

 

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

 

 




