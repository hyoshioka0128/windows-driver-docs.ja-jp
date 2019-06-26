---
title: IPsec オフロードでのネットワーク インターフェイスの変更の影響
description: IPsec オフロードでのネットワーク インターフェイスの変更の影響
ms.assetid: 7d1b2bf9-31a9-4fc4-92f3-dc7b5e0277e3
keywords:
- WDK IPsec オフロード、ESP により保護されたパケットをルーティング インターフェイスの変更
- WDK IPsec オフロード AH で保護されたパケットをルーティング インターフェイスの変更
- WDK の IPsec ESP により保護されたパケットのオフロード、NIC を削除し、
- AH で保護されたパケット WDK IPsec オフロード、NIC を削除し、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfa670125e2434df158e1b9340741b1688ca1705
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369202"
---
# <a name="impact-of-network-interface-changes-on-ipsec-offloads"></a>IPsec オフロードでのネットワーク インターフェイスの変更の影響

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




ネットワーク インターフェイスには、次のイベントは、インターネット プロトコル セキュリティ (IPsec) タスクのオフロードに影響します。

-   NIC が削除されます。

    ミニポート ドライバーが NIC からすべてのセキュリティ アソシエーション (Sa) を削除する必要があります、システムからタスクがオフロードされている NIC を削除する前に ミニポート ドライバーは、TCP/IP トランスポートが、SAs を削除することを要求する必要はありません。

-   ルーティング インターフェイスが変更されます。

    ネットワーク トラフィックは、新しいインターフェイスを介してルーティングは、適切な SAs が新しいインターフェイスで使用される NIC に追加されるまで、TCP/IP スタックが一時的に IPsec タスクを実行します。 TCP/IP スタックを発行してに SA を NIC に追加する[OID\_TCP\_タスク\_IPSEC\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-sa)します。 以前のインターフェイスに使用される NIC での SAs の後に有効期限が切れる、TCP/IP トランスポート問題[OID\_TCP\_タスク\_IPSEC\_削除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-sa)同じ回数NIC から NIC のミニポート ドライバーが、SAs を削除することを要求するために必要

 

 





