---
title: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME
description: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME は、Wi-Fi Direct パブリック アクション フレーム要求を送信するデバイスに発行されます。
ms.assetid: bd8a746e-7d47-44c1-ad05-a452ce00749f
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 27a8953f5308cec9a9187c27a9f1fce21c3896ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387233"
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

## <a name="validation"></a>［確認］

WDI をサポートするミニポート ドライバーのバージョン 1.1.8 と発信の P2P アクション フレームの P2P IEs の以降では、追加の検証が追加されました。 この検証を一般的な問題に対処して、**構成タイムアウト**P2P IE の属性が OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME とLEに提供する(ミリ秒単位)の形式を変換単位されていません[OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md)、数十ミリ秒の単位に IE の形式であります。

WDI バージョン 1.1.8 と以降の場合をサポートしているドライバーの Wi-Fi Direct と Wi-Fi Direct サービス HLK テストが失敗、**構成タイムアウト**P2P IE の属性が、送信アクション フレームに対して正しくエンコードされていません。 WDI バージョン 1.1.7 のテストがテスト出力に警告を表示する前と。

WDI インターフェイス自体は変更されずは引き続き以前と同様、1.1.7 のバージョンは、ミリ秒の単位を使用しています。

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-send-action-request-frame-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-send-action-request-frame-parameters)"><strong>WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>フレームのアクションの種類、対象のピア アダプター、およびダイアログのトークンのデバイスのアドレスなどのパラメーター。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-go-negotiation-request-info" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-go-negotiation-request-info)"><strong>WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>x</td>
<td>ネゴシエーション要求パラメーターを参照してください。 WfdRequestFrameType がネゴシエーションの移動要求の場合、ポートだけこの構造体で検証されます。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-invitation-request-info" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INVITATION_REQUEST_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-invitation-request-info)"><strong>WDI_TLV_P2P_INVITATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>x</td>
<td>招待要求のパラメーターです。 ポートは、wfdRequestFrameType は招待要求を場合、この構造体を調べるだけ必要があります。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-provision-discovery-request-info" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-provision-discovery-request-info)"><strong>WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO</strong></a></td>
<td></td>
<td>x</td>
<td>プロビジョニングの検出要求のパラメーターです。 WfdRequestFrameType が、プロビジョニングの検出要求の場合ポートだけこの構造体で検証されます。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_BSS_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry)"><strong>WDI_TLV_BSS_ENTRY</strong></a></td>
<td></td>
<td></td>
<td><p>ポートから Wi-Fi Direct 検出タスクによって返されるデバイスの検出エントリ。</p>
<p>これは、ポートは、探索を必要とせず、リモート Wi-Fi Direct デバイスに Wi-Fi Direct アクション フレームの要求を送信するには、探索データベースを記憶する必要はありませんのでに提供されます。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>x</td>
<td>ポートによって送信されたフレームに含める必要がある 1 つまたは複数の i。</td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_P2P\_送信\_要求\_アクション\_フレーム\_完了](ndis-status-wdi-indication-p2p-send-request-action-frame-complete.md)

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

 

 




