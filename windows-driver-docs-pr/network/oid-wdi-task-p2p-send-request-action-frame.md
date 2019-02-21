---
title: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME
description: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME は、Wi-Fi Direct パブリック アクション フレーム要求を送信するデバイスに発行されます。
ms.assetid: bd8a746e-7d47-44c1-ad05-a452ce00749f
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 48b49b8c11dc91aaca2297727f927f5a8338a9d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560538"
---
# <a name="oidwditaskp2psendrequestactionframe"></a>OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレーム


OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレームは、Wi-Fi Direct パブリック アクション フレーム要求を送信するデバイスに発行します。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 3                                     | 5                               |

 

このコマンドは、異なる[OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレーム](oid-wdi-task-p2p-send-response-action-frame.md)、これは、大幅に多くの時間を区別する操作です。

要求フレームの受信確認を受信すると、デバイスは 100 ミリ秒の同じチャネルについて熟考し、フレームを示す、Wi-Fi Direct パブリック アクション、ホストに受信しました。

最大のタイムアウトの期限が切れていないときに、デバイスは、リモート デバイスのリッスン チャネル上のリモート デバイスに Wi-Fi Direct パブリック アクション フレームを送信する再試行してください。

タスクが完了するかローカルのデバイスが送信された操作フレーム用のリモート デバイスから受信確認を受信すると、タイムアウトになると、または、ホストは、操作を中止します。 デバイスは、同じチャネル時間の有効期限が切れた後、タスクの完了にすることがあります。

ホストは、この操作を中止し、続行/再試行、Wi-Fi Direct アクション フレーム交換できるようになりますが、デバイスがすぐにこの操作を中止することがある重要なことがあります。

## <a name="task-parameters"></a>タスク パラメーター


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898001" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898001)"><strong>WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>フレームのアクションの種類、対象のピア アダプター、およびダイアログのトークンのデバイスのアドレスなどのパラメーター。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897937" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897937)"><strong>WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>ネゴシエーション要求パラメーターを参照してください。 WfdRequestFrameType がネゴシエーションの移動要求の場合、ポートだけこの構造体で検証されます。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897963" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INVITATION_REQUEST_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897963)"><strong>WDI_TLV_P2P_INVITATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>招待要求のパラメーターです。 ポートは、wfdRequestFrameType は招待要求を場合、この構造体を調べるだけ必要があります。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897980" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897980)"><strong>WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>プロビジョニングの検出要求のパラメーターです。 WfdRequestFrameType が、プロビジョニングの検出要求の場合ポートだけこの構造体で検証されます。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926162" data-raw-source="[&lt;strong&gt;WDI_TLV_BSS_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926162)"><strong>WDI_TLV_BSS_ENTRY</strong></a></td>
<td></td>
<td></td>
<td><p>ポートから Wi-Fi Direct 検出タスクによって返されるデバイスの検出エントリ。</p>
<p>これは、ポートは、探索を必要とせず、リモート Wi-Fi Direct デバイスに Wi-Fi Direct アクション フレームの要求を送信するには、探索データベースを記憶する必要はありませんのでに提供されます。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898076" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898076)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>X</td>
<td>ポートによって送信されたフレームに含める必要がある 1 つまたは複数の i。</td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_P2P\_送信\_要求\_アクション\_フレーム\_完了](ndis-status-wdi-indication-p2p-send-request-action-frame-complete.md)要件
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

 

 




