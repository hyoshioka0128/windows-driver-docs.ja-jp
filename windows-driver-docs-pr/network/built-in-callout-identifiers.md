---
title: 組み込みのコールアウト識別子
description: このセクションでは、組み込みのコールアウト識別子について説明します。
ms.assetid: c0200388-1e79-41b9-890c-ce0034b329d8
keywords:
- 組み込みのコールアウト識別子ネットワーク ドライバー
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: af466e48be6c13231bf9b76e389e5ff8a53ded14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550845"
---
# <a name="built-in-callout-identifiers"></a>組み込みのコールアウト識別子

Windows フィルタ リング プラットフォームに組み込まれているコールアウトの識別子は、各 GUID で表されます。 これらの識別子の定義は次のとおりです。

> [!NOTE]
> コールアウト識別子の末尾に V4 および V6 サフィックスでは、引き出し線は、IPv4 ネットワーク スタックまたは IPv6 ネットワーク スタックにかどうかを示します。

| 組み込みのコールアウトの識別子 | コールアウトの説明 |
| --- | --- |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_TRANSPORT_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_TRANSPORT_V6</p> | トランスポート モード セキュリティ アソシエーション経由で到着することになっている各受信パケットが安全に到着したことを確認します。 この吹き出しは、トランスポート層で適用されます。 |
| <p>FWPM_CALLOUT_IPSEC_OUTBOUND_TRANSPORT_V4</p><p>FWPM_CALLOUT_IPSEC_OUTBOUND_TRANSPORT_V6</p> | IPsec トランスポート モード セキュリティ アソシエーションによってセキュリティで保護する必要がありますが、発信トラフィックを示します。 この吹き出しは、トランスポート層で適用されます。 |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_TUNNEL_V6</p> | トンネル モード セキュリティ アソシエーション経由で到着することになっている各受信パケットが安全に到着したことを確認します。 この吹き出しは、トランスポート層で適用されます。 |
| <p>FWPM_CALLOUT_IPSEC_OUTBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_OUTBOUND_TUNNEL_V6</p> | IPsec トンネル モード セキュリティ アソシエーションによってセキュリティで保護する必要がありますが、発信トラフィックを示します。 この吹き出しは、トランスポート層で適用されます。 |
| <p>FWPM_CALLOUT_IPSEC_FORWARD_INBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_FORWARD_INBOUND_TUNNEL_V6</p> | トンネル モード セキュリティ アソシエーション経由で到着することになっている各受信パケットが安全に到着したことを確認します。 この吹き出しは、前方の層に適用されます。 |
| <p>FWPM_CALLOUT_IPSEC_FORWARD_OUTBOUND_TUNNEL_V4</p><p>FWPM_CALLOUT_IPSEC_FORWARD_OUTBOUND_TUNNEL_V6</p> | IPsec トンネル モード セキュリティ アソシエーションによってセキュリティで保護する必要がありますが、発信トラフィックを示します。 この吹き出しは、前方の層に適用されます。 |
| <p>FWPM_CALLOUT_IPSEC_INBOUND_INITIATE_SECURE_V4</p><p>FWPM_CALLOUT_IPSEC_INBOUND_INITIATE_SECURE_V6</p> | 安全に到着することは想定されている各受信接続はそのことを確認します。 この吹き出しは ALE で該当するレイヤーをそのまま使用します。 |
| <p>FWPM_CALLOUT_IPSEC_ALE_CONNECT_V4</p><p>FWPM_CALLOUT_IPSEC_ALE_CONNECT_V6</p> | クライアント アプリケーションには、IPsec ポリシーの修飾子を適用します。 |
| <p>FWPM_CALLOUT_WFP_TRANSPORT_LAYER_V4_SILENT_DROP</p><p>FWPM_CALLOUT_WFP_TRANSPORT_LAYER_V6_SILENT_DROP</p> | サイレント モードで TCP がリッスンしているエンドポイントにないすべての受信パケットを削除します。 この吹き出しは、受信トランスポート層に適用されます。 |
| <p>FWPM_CALLOUT_TCP_CHIMNEY_CONNECT_LAYER_V4</p><p>FWPM_CALLOUT_TCP_CHIMNEY_CONNECT_LAYER_V6</p> | 有効または各送信接続の TCP chimney オフロードを無効にします。 |
| <p>FWPM_CALLOUT_TCP_CHIMNEY_ACCEPT_LAYER_V4</p><p>FWPM_CALLOUT_TCP_CHIMNEY_ACCEPT_LAYER_V6</p> | 有効または、各受信接続の TCP chimney オフロードを無効にします。 |

