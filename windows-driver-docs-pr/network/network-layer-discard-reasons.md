---
title: ネットワーク レイヤー破棄理由
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーをネットワーク レイヤー破棄理由について説明します。 |
ms.assetid: 30066077-53ac-43bb-8c8b-67af210f747e
keywords:
- ネットワーク層上の理由からネットワーク ドライバーを破棄します。
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc51c3ca5788497cd7d005e740aae8e31fa61c2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536738"
---
# <a name="network-layer-discard-reasons"></a>ネットワーク レイヤー破棄理由

識別子のネットワーク層のいずれかによってデータが破棄された原因には次のとおりです。 これらの識別子は、Fwpsk.h で定義されている IP_DISCARD_REASON 列挙で定数の値です。

| 理由の識別子を破棄します。 | 理由の説明を破棄します。 |
| --- | --- |
| IpDiscardBadSourceAddress | 発信パケットの送信元アドレスがマルチキャスト アドレスをブロードキャスト アドレス、または埋め込みの IPv4 ループバックを含む IPv6 アドレスまたはアドレスが指定されていません。 |
| IpDiscardNotLocallyDestined | システムで、受信パケットの宛先アドレスが存在しないため、適切な転送インターフェイスが存在しません。 |
| IpDiscardProtocolUnreachable | 受信したパケットのどちらもトランスポート プロトコル ハンドラーがあるか、トランスポート プロトコル ハンドラーが、パケットの処理を拒否しました。 |
| IpDiscardPortUnreachable | 受信パケットの宛先ポート上のパケットを受信しているアプリケーションはありません。 |
| IpDiscardBadLength | 受信したパケット内で指定された長さフィールドでは、パケットの長さと一致しません。 |
| IpDiscardMalformedHeader | 受信パケットには、認識されている拡張機能のヘッダーまたはオプションが有効でない内容が含まれています。 |
| IpDiscardNoRoute | システムのルーティング テーブルにその先へのルートが含まれていないために、受信したパケットを宛先アドレスに転送できません。 |
| IpDiscardBeyondScope | パケットの受信および送信のネットワーク インターフェイスがパケットのゾーン レベルの異なるゾーン インデックスがあるために、受信したパケットを転送できません。 |
| IpDiscardInspectionDrop | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardTooManyDecapsulations | Decapsulations が多すぎますがあるために、受信パケットを宛先アドレスに転送できません。 |
| IpDiscardAdministrativelyProhibited | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardHopLimitExceeded | 受信パケットのホップの制限または有効期限の制限を超えました。 |
| IpDiscardAddressUnreachable | 発信パケット送信できませんパケットの宛先アドレスにか、変換先がいないため、存在するか、またはその送信先に送信されるパケットは許可されていません。 |
| IpDiscardRscPacket | 受信側のまとめられた (RSC) パケットである送信パケットを送信できません。 |
| IpDiscardArbitrationUnhandled | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardInspectionAbsorb | WFP は、パケットの所有権を取得しました。 発信パケットを送信できません。 |
| IpDiscardDontFragmentMtuExceeded | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardBufferLengthExceeded | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardAddressResolutionTimeout | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardAddressResolutionFailure | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardIpsecFailure | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardExtensionHeadersFailure | ネットワーク スタックによって、内部使用のため予約されています。 |
| IpDiscardAllocationFailure | ネットワーク スタックによって、内部使用のため予約されています。 |

