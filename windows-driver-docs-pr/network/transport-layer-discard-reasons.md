---
title: トランスポート層の破棄の理由
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーのトランスポート層の破棄理由について説明します。
ms.assetid: e2a9dcd1-87c6-4052-ae96-3a7994328dd0
keywords:
- トランスポート層上の理由からネットワーク ドライバーを破棄します。
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5008e6eb284ba76b671909b1e1a01aeed12fe001
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537539"
---
# <a name="transport-layer-discard-reasons"></a>トランスポート層の破棄の理由

識別子のトランスポート層のいずれかによってデータが破棄された原因には次のとおりです。 これらの識別子は、Fwpsk.h で定義されている INET_DISCARD_REASON 列挙で定数の値です。

| 理由の識別子を破棄します。 | 理由の説明を破棄します。 |
| --- | --- |
| InetDiscardSourceUnspecified | 発信パケットの送信元アドレスが指定されていません。 |
| InetDiscardDestinationMulticast | 発信パケットの宛先アドレスが指定されていないアドレスであり、トランスポートはマルチキャスト アドレスをサポートしていません。 |
| InetDiscardHeaderInvalid | パケットのトランスポート プロトコルのヘッダーが無効です。 |
| InetDiscardChecksumInvalid | パケットのトランスポート プロトコルのヘッダーでチェックサムが無効です。 |
| InetDiscardEndpointNotFound | パケットのヘッダーで指定されたエンドポイントが見つかりませんでした。 |
| InetDiscardConnectedPath | パケットのリモート アドレスは、リモート接続済みのエンドポイントのアドレスと一致しません。 |
| InetDiscardSessionState | パケットはネットワーク層の情報に基づいて提供ことはできません。 |
| InetDiscardReceiveInspection | 受信検査に失敗したため、接続が閉じられました。 |
| InetDiscardAckInvalid | パケットには、無効な ACK セグメントです。 |
| InetDiscardExpectedSyn | SYN セグメントが必要です。 |
| InetDiscardRst | パケットには、無効な RST セグメントです。 |
| InetDiscardSynRcvdSyn | SYN_RCVD 状態の TCP 接続は、別の SYN セグメントを受信しました。 |
| InetDiscardSimultaneousConnect | TCP 接続は、simultaneous-connect 条件が発生しました。 |
| InetDiscardPawsFailed | TCP の PAW のチェックに失敗しました。 |
| InetDiscardLandAttack | パケットが Land 攻撃の一部として検出されました。 |
| InetDiscardMissedReset | SYN_RCVD 接続で受信ウィンドウの外側の SYN セグメントを受信しました。 RST が見つからなかった可能性があります。 |
| InetDiscardOutsideWindow | TCP セグメントは、受信ウィンドウ外にありました。 |
| InetDiscardDuplicateSegment | 重複している TCP セグメントが受信されました。 |
| InetDiscardClosedWindow | TCP 受信ウィンドウが閉じられました。 |
| InetDiscardTcbRemoved | TCP 接続が閉じられました。 |
| InetDiscardFinWait2 | TCP 接続を終了しています。 |
| InetDiscardReassemblyConflict | FIN セグメントの受信 TCP データの再構築の競合が発生しました。 |
| InetDiscardFinReceived | FIN は、TCP 接続は既に受信以上のデータを受信できます。 |
| InetDiscardListenerInvalidFlags | 無効なフラグでのセグメントは、待機中の TCP ソケットによって受信されました。 |
| InetDiscardUrgentDeliveryAllocationFailure | TCP 接続で URG 配信が不足しているメモリです。 |
| InetDiscardTcbNotInTcbTable | 緊急の配信のための TCP 接続を閉じました。 |
| InetDiscardTimeWaitTcbReceivedRstOutsideWindow | TIME_WAIT 状態の TCP 接続は、ウィンドウの外側、RSP セグメントを受信しました。 |
| InetDiscardTimeWaitTcbSynAndOtherFlags | TIME_WAIT 状態の TCP 接続が受信したは、SYN セグメントと互換性のない 1 つまたは複数のフラグ。 |
| InetDiscardTimeWaitTcb | TIME_WAIT 状態の TCP 接続を受信セグメントが無効です。 |

