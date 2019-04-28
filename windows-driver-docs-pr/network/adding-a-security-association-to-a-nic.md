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
ms.openlocfilehash: 019d8e39122590adccff5570e4ba8b9933f21c3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367846"
---
# <a name="adding-a-security-association-to-a-nic"></a>NIC へのセキュリティ アソシエーションの追加

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




トランスポートは、NIC がインターネット プロトコル セキュリティ (IPsec) の操作を実行できることを決定後、TCP/IP (を参照してください[NIC の IPsec 機能を Reporting](reporting-a-nic-s-ipsec-capabilities.md))、トランスポートは、1 つまたは複数の受信を追加する NIC のミニポート ドライバーを要求する必要があります送信セキュリティ アソシエーション (Sa) とトランスポート NIC には、NIC に IPsec タスク オフロードできますと ミニポート ドライバーが、TCP/IP をトランスポート設定、NIC に 1 つ以上の SAs を追加することを要求する[OID\_TCP\_タスク\_IPSEC\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569808)します。

 

 





