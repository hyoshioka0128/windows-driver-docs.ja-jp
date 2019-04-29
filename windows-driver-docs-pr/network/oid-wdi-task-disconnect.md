---
title: OID_WDI_TASK_DISCONNECT
description: OID_WDI_TASK_DISCONNECT を使用して、ピアとの接続を終了します。
ms.assetid: 03566fbd-5043-4166-bd33-0ed48f85f370
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_DISCONNECT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a18882adea48a6e9c4256e4cf6aa11a1450f00ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383591"
---
# <a name="oidwditaskdisconnect"></a>OID\_WDI\_タスク\_切断


OID\_WDI\_タスク\_切断は、ピアとの接続を終了するために使用します。

| オブジェクト | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------|---------------------------------------|---------------------------------|
| ポート   | X            | 2                                     | 1                               |

 

このコマンドは、アクセス ポイントや、Wi-Fi Direct 移動から切断し、ポートのクライアントを切断するに使用されます。 切断が受信されると、ポートでの関連付けを解除し、ピアから deauthenticate し、そのピアに関連付けられている状態をクリアする必要があります。 ただし、その必要がありますリセットされませんこのピアに固有ではない接続パラメーターのいずれか。 切断のアクティビティが完了した後にのみ、タスクを完了する必要があります。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                            | 許可されている複数の TLV インスタンス | 省略可能 | 説明                |
|--------------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI\_TLV\_切断\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926300) |                                |          | 切断のパラメーター。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_切断\_完了](ndis-status-wdi-indication-disconnect-complete.md)
## <a name="unsolicited-indication"></a>要請されていないを示す値


[NDIS\_状態\_WDI\_を示す値\_関連付け解除](ndis-status-wdi-indication-disassociation.md)ポート、ネットワークから接続が切断された、OS に、関連付けの解除を示す値を送信します。 [切断]、OS からのコマンドをトリガーするまたはネットワークから発生する可能性があります。 トリガーされたネットワーク切断を 5 月から関連付け解除または deauthentication のパケットの受信を明示的に指定するか、ポートに接続されているピアのプレゼンスを検出できないときに暗黙的な可能性があります。

ポートは、関連付けの解除を示す値が送信される前に、ピアに関連付けられている状態を消去する必要があります。 これには、任意のキーと、ピアに関連付けられている 802.1 x ポート承認情報が含まれます。 ポートでは、単独でのローミングがトリガーされない必要があります。

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

 

 




