---
title: NIC へのセキュリティ アソシエーションの追加
description: NIC へのセキュリティ アソシエーションの追加
ms.assetid: 524cc9f8-fe02-4192-85af-83813ae83d08
keywords:
- セキュリティ アソシエーション WDK IPsec オフロードします。
- SAs の WDK IPsec オフロード
- WDK の IPsec ESP により保護されたパケットのオフロード、セキュリティ アソシエーション
- AH で保護されたパケット WDK IPsec オフロード、セキュリティ アソシエーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc4c279bdd78dafe37a7528cc35fa77f921279c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384731"
---
# <a name="adding-a-security-association-to-a-nic"></a>NIC へのセキュリティ アソシエーションの追加

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




トランスポートは、NIC がインターネット プロトコル セキュリティ (IPsec) の操作を実行できることを決定後、TCP/IP (を参照してください[NIC の IPsec 機能を Reporting](reporting-a-nic-s-ipsec-capabilities.md))、トランスポートは、1 つまたは複数の受信を追加する NIC のミニポート ドライバーを要求する必要があります送信セキュリティ アソシエーション (Sa) とトランスポート NIC には、NIC に IPsec タスク オフロードできますと ミニポート ドライバーが、TCP/IP をトランスポート設定、NIC に 1 つ以上の SAs を追加することを要求する[OID\_TCP\_タスク\_IPSEC\_追加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-sa)します。

 

 





