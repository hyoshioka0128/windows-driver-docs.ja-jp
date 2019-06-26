---
title: OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME
description: ピアに、Wi-Fi Direct パブリック アクション フレーム要求を送信する IHV コンポーネントに OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME が発行されます。
ms.assetid: 5cb57f20-ef9d-4e79-9b4b-8cf939221d47
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 28052e758d5951ac77eb1e0e13bbd6341d0f9ca5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387231"
---
# <a name="oidwditaskp2psendresponseactionframe"></a>OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレーム


OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレームは、ピアに、Wi-Fi Direct パブリック アクション フレーム要求を送信する IHV コンポーネントに発行します。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 3                                     | 5                               |

 

要求のフレームの受信確認を受信すると、ポートは 100 ミリ秒の同じチャネルについて熟考し、フレームを示す、Wi-Fi Direct パブリック アクション、ホストに受信しました。

このタスクは、時間に依存します。 Wi-Fi Direct 送信アクションに対する応答はのみ処理されるこのパケットの受信の 100 ミリ秒以内、Wi-Fi Direct 仕様が必要です。

最大のタイムアウトの期限が切れていないときに、ポートが次の表で定義されているの適切なチャネル上のリモート デバイスに Wi-Fi Direct 送信を再試行するものとします。 テーブルは、コマンドが実行されたときに、パケットを送信する先の明示的なチャネルの要件を定義します。 一般的な規則は、以前の要求と同じチャネルで応答パケットが送信です。

| 応答アクションのフレームの種類   | ターゲットの送信チャネル                               |
|------------------------------|-------------------------------------------------------|
| ネゴシエーション応答を移動します。      | ローカル リッスン チャネル                                  |
| ネゴシエーションの確認を参照してください。  | リモート受信チャネル                                 |
| 招待の応答          | ローカルのリッスンまたはローカルの移動の操作チャネル          |
| プロビジョニングの検出の応答 | 稼動チャネルがリッスン チャネルのローカルまたはリモートの移動 |

 

タスクが完了するかローカル デバイス送信された操作フレーム用のリモート デバイスからの受信確認を受信すると、タイムアウトになると、またはホストは、操作を中止します。 デバイスは、同じチャネル時間の有効期限が切れた後、タスクの完了にすることがあります。

ホストは、この操作を中止し、続行/再試行、Wi-Fi Direct アクション フレーム交換できるようになりますが、デバイスがすぐにこの操作を中止することがある重要なことがあります。

## <a name="validation"></a>［確認］

WDI をサポートするミニポート ドライバーのバージョン 1.1.8 と発信の P2P アクション フレームの P2P IEs の以降では、追加の検証が追加されました。 この検証を一般的な問題に対処して、**構成タイムアウト**P2P IE の属性が (ミリ秒単位) の形式を変換単位で LE に提供する[OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md)と IE 形式である OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME、数十ミリ秒の単位にします。

WDI バージョン 1.1.8 と以降の場合をサポートしているドライバーの Wi-Fi Direct と Wi-Fi Direct サービス HLK テストが失敗、**構成タイムアウト**P2P IE の属性が、送信アクション フレームに対して正しくエンコードされていません。 WDI バージョン 1.1.7 のテストがテスト出力に警告を表示する前と。

WDI インターフェイス自体は変更されずは引き続き以前と同様、1.1.7 のバージョンは、ミリ秒の単位を使用しています。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_ACTION\_FRAME\_RESPONSE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-action-frame-response-parameters)   |                                |          | フレームのアクションの種類、対象のピア アダプター、およびダイアログのトークンのデバイスのアドレスなどのパラメーター。                                                 |
| [**WDI\_TLV\_P2P\_GO\_NEGOTIATION\_RESPONSE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-go-negotiation-response-info)           |                                | x        | ネゴシエーション応答のパラメーターを参照してください。 WfdRequestFrameType が移動のネゴシエーション応答の場合、ポートだけこの構造体で検証されます。            |
| [**WDI\_TLV\_P2P\_移動\_ネゴシエーション\_確認\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-go-negotiation-confirmation-info)   |                                | x        | ネゴシエーション確認パラメーターを参照してください。 WfdRequestFrameType が移動のネゴシエーション確認の場合、ポートだけこの構造体で検証されます。    |
| [**WDI\_TLV\_P2P\_INVITATION\_RESPONSE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-invitation-response-info)                    |                                | x        | 招待の応答のパラメーター。 WfdRequestFrameType が応答を場合、ポートはこの構造体を調べるだけ必要があります。                   |
| [**WDI\_TLV\_P2P\_プロビジョニング\_検出\_応答\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-provision-discovery-response-info) |                                | x        | 検出応答のパラメーターをプロビジョニングします。 WfdRequestFrameType がプロビジョニング検出の応答の場合、ポートはこの構造を調べてのみものとします。 |
| [**WDI\_TLV\_P2P\_受信\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-incoming-frame-information)                |                                |          | 以前に受信した P2P アクション フレームから指定された情報です。 ポートに受信した指示が提供されます。            |
| [**WDI\_TLV\_ベンダー\_特定\_IE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie)                                         |                                | x        | ポートによって送信されたフレームに含める必要がある 1 つまたは複数の i。                                                                           |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_STATUS\_WDI\_INDICATION\_P2P\_SEND\_RESPONSE\_ACTION\_FRAME\_COMPLETE](ndis-status-wdi-indication-p2p-send-response-action-frame-complete.md)

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

 

 




