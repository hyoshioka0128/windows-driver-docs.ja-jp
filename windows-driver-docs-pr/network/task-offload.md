---
title: TCP/IP タスク オフロード
description: TCP/IP タスク オフロード
ms.assetid: e73cc4e8-574b-438b-acd2-f0aaf5c20589
keywords:
- TCP/IP のオフロード WDK のネットワー キング、タスクのオフロード
- WDK TCP/IP トランスポート、タスク オフロードをオフロードします。
- タスクのオフロード WDK TCP/IP トランスポート
- タスクのオフロード WDK TCP/IP トランスポートは、タスク オフロードの詳細について
- 機能 WDK TCP/IP の負荷を軽減します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb2d2343f1cedb336344ac53cc2f749f562605e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580155"
---
# <a name="tcpip-task-offload"></a>TCP/IP タスク オフロード





パフォーマンスを向上させるには、Microsoft TCP/IP トランスポートを適切なタスクをオフロード機能を持つネットワーク インターフェイス カード (NIC) にタスクをオフロードできます。

以降、Windows Vista、Windows オペレーティング システムがサポートでは、次のタスクのオフロード サービス。

### <a name="checksum-tasks"></a>チェックサム タスク

TCP/IP トランスポートは、計算と ip アドレスと TCP チェックサムの検証をオフロードできます。

### <a name="internet-protocol-security-ipsec-offload-version-1-ipsecov1"></a>インターネット プロトコル セキュリティ (IPsec) の負荷を軽減バージョン 1 (IPsecOV1)

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

TCP/IP トランスポートは、計算とセキュリティ ペイロード (ESP)、またはその両方をカプセル化する、認証ヘッダー (AH) の暗号化チェックサムの検証をオフロードできます。 TCP/IP トランスポートも、暗号化と ESP ペイロードの暗号化解除と暗号化とユーザー データグラム プロトコル (UDP) の復号化をオフロードできます-ESP データ パケットをカプセル化します。

IPsecOV1 の詳細については、[IPsec オフロード バージョン 1](ipsec-offload-version-1.md)を参照してください。

### <a name="internet-protocol-security-ipsec-offload-version-2-ipsecov2"></a>インターネット プロトコル セキュリティ (IPsec) の負荷を軽減バージョン 2 (IPsecOV2)

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]

TCP/IP トランスポートは、計算とセキュリティ ペイロード (ESP)、またはその両方をカプセル化する、認証ヘッダー (AH) の暗号化チェックサムの検証をオフロードできます。 TCP/IP トランスポートも、暗号化と ESP ペイロードの暗号化解除と暗号化とユーザー データグラム プロトコル (UDP) の復号化をオフロードできます-ESP データ パケットをカプセル化します。 IPsecOV2 は NDIS 6.1 以降でサポートされています。

IPsecOV2 の詳細については、[IPsec オフロード バージョン 2](ipsec-offload-version-2.md)を参照してください。

### <a name="large-send-offload-version-1-lsov1"></a>大量送信オフロード バージョン 1 (LSOV1)

TCP/IP トランスポートは、大量送信オフロード バージョン 1 (LSOV1) をサポートします。 TCP/IP トランスポートは LSOV1 に大きな (最大 64 kb の IP ヘッダーを含む) のセグメント化をオフロードすることができますの IPv4 TCP パケット。

### <a name="large-send-offload-version-2-lsov2"></a>大量送信オフロード バージョン 2 (LSOV2)

大量の送信は、バージョン 2 (LSOV2) インターフェイスが LSOV1 の拡張のバージョンをオフロードします。 LSOV2 は 64 K より大きな TCP パケットの IPv6、IPv4、およびセグメント化をサポートします。 大きなパケットのセグメント化オフロードの詳細については、[、セグメント化の大きな TCP パケットのオフロード](offloading-the-segmentation-of-large-tcp-packets.md)を参照してください。

Windows 8 および Windows Server 2012 以降、Windows オペレーティング システムには、次の追加のタスクのオーバー ロードのサービスがサポートされています。

### <a name="receive-segment-coalescing-rsc"></a>Receive Segment Coalescing (RSC)

Coalescing (RSC) 有効のネットワーク カードのミニポート ドライバーは複数の TCP セグメントを結合し、オペレーティング システムのネットワーク サブシステムにまとめられた 1 つの単位 (SCU) として示すためにセグメントが表示されます。

### <a name="network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>汎用ルーティング カプセル化 (NVGRE) タスク オフロードを使用したネットワークの仮想化

[ネットワーク仮想化の Generic Routing Encapsulation (NVGRE) タスク オフロードを使用して](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)Generic Routing Encapsulation GRE カプセル化パケットを使用することになります。

-   Large Send Offload (LSO)
-   Receive Side Scaling (RSS)
-   仮想マシン キュー (VMQ)

このセクションの内容:

-   [タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)
-   [オフロード サービスを有効にして、タスクを無効化](enabling-and-disabling-task-offload-services.md)
-   [現在のタスクのオフロード設定を決定します。](determining-the-current-task-offload-settings.md)
-   [タスクの型を結合する負荷を軽減します。](combining-types-of-task-offloads.md)
-   [レジストリ値を使用してタスク オフロードを無効にするには](using-registry-values-to-enable-and-disable-task-offloading.md)
-   [チェックサム タスクをオフロードします。](offloading-checksum-tasks.md)
-   [IPsec タスクをオフロード](offloading-ipsec-tasks.md)
    - \[IPsec タスク オフロード機能は非推奨し、は使用できません。\]
-   [大きな TCP パケットのセグメント化をオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

 

 





