---
title: UDP カプセル化 ESP パケットを使用した NAT と NAPT の走査
description: UDP カプセル化 ESP パケットを使用した NAT と NAPT の走査
ms.assetid: 9bfd6a7c-2c24-419e-b82d-ef6ef8fe1fa5
keywords:
- WDK の IPsec ESP パケットを UDP カプセル化オフロード、transversing Nat NAPTs
- ネットワーク アドレス変換器 WDK IPsec オフロードします。
- ネットワーク アドレスのポート変換器 WDK IPsec オフロードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f8bc04aa31a8c1cc08607571dff3c3937045111
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368454"
---
# <a name="traversing-nats-and-napts-with-udp-encapsulated-esp-packets"></a>UDP カプセル化 ESP パケットを使用した NAT と NAPT の走査

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




ネットワーク アドレス変換器 (Nat) とネットワーク アドレスのポート変換器 (NAPTs) できるため、単一の IP アドレスを共有する多くのシステムを複数のプライベート ネットワーク アドレスを 1 つのルーティング IP パブリック アドレスにし、その逆に変換します。 これにより、Nat と NAPTs ルーティングの IPv4 アドレスの不足を軽減するために役立ちます。

ただし、Nat と NAPTs によって、インターネット プロトコル セキュリティ (IPsec) で問題が発生することができます。 Nat と NAPTs パケットの IP ヘッダーを変更するため、チェックサムの検証に失敗する AH で保護されたパケットが発生します。 NAPTs、TCP および UDP ポートの変更は、ESP により保護されたパケットの暗号化された TCP ヘッダー内のポートを変更することはできません。

UDP カプセル化では、この問題は解決します。 実際には、UDP カプセル化が ESP パケットでのみ使用されます。 NAT または NAPT には、重大な ESP の認証と ESP 暗号化によって苦労しましたされることがなく、ESP の UDP カプセル化パケットの暗号化されていない ip アドレスと UDP ヘッダーを変更できます。 ESP パケットの UDP カプセル化の詳細については、次を参照してください。 [UDP カプセル化の理由を NAT 経由での IPsec](https://go.microsoft.com/fwlink/p/?linkid=9856)します。

Microsoft では、ポート 4500 を ESP パケットの UDP カプセル化をサポートします。 IKE はピア ポート 500 のネゴシエーションを開始、NAT トラバーサルをサポートの検出しパスに沿った NAT または NAPT を検出、"float"IKE と UDP の ESP トラフィックをポート 4500 をネゴシエートすることができます。 このネゴシエーションの詳細については、次を参照してください。[ネゴシエーションの Nat-traversal ike](https://go.microsoft.com/fwlink/p/?linkid=9857)します。

浮動小数点ポート 4500 NAT トラバーサルをからには、次の利点が提供されます。

-   「IPsec 対応」の Nat またはポート 500 で UDP ESP カプセル化を中断 NAPTs をバイパスします。

-   パフォーマンスが向上します。 ESP データ パケットの UDP カプセル化は、ポート 500 でポート 4500 よりも効率的です。 詳細については、次を参照してください。 [UDP ESP カプセル化型](udp-esp-encapsulation-types.md)します。

UDP ESP カプセル化をサポートするために、ミニポート ドライバーまたは NIC (またはその両方) があります。

-   」の説明に従って、受信パスで ESP パケットを処理することができる[受信パスでの IPsec タスク オフロード](offloading-ipsec-tasks-in-the-receive-path.md)します。

-   パーサーのエントリの一覧を維持します。 パーサーのエントリには、NIC が 1 つまたは複数のセキュリティ アソシエーション (Sa) の入力方向の UDP ESP パケットを解析が必要な情報が含まれています。 パーサーのエントリに関する詳細については、次を参照してください。 [UDP ESP SAs とパーサー エントリ](udp-esp-sas-and-parser-entries.md)します。

-   トランスポートが NIC にオフロードされた SAs のリストを維持します。

-   次の Oid をサポートしてください。
    -   [OID\_TCP\_TASK\_IPSEC\_ADD\_UDPESP\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-udpesp-sa)
    -   [OID\_TCP\_タスク\_IPSEC\_削除\_UDPESP\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-udpesp-sa)

 

 





