---
title: UDP ESP パケットを解析する NIC の機能の報告、有効化、無効化
description: UDP ESP パケットを解析する NIC の機能の報告、有効化、無効化
ms.assetid: 3a75c5b2-2d94-428e-9b2a-d760e14df552
keywords:
- UDP カプセル化 ESP パケット WDK IPsec オフロード、解析機能
- 解析機能 WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9aee749b2315a7675aa95c73d0879619245677f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842053"
---
# <a name="reporting-enabling-and-disabling-a-nics-ability-to-parse-udp-esp-packets"></a>UDP ESP パケットを解析する NIC の機能の報告、有効化、無効化

\[IPsec タスクオフロード機能は非推奨とされているため、使用しないでください。\]




ミニポートドライバーは、 [**NDIS\_ipsec\_オフロード\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)構造体の NIC のインターネットプロトコルセキュリティ (ipsec) 機能を指定します。 詳細については、「 [NIC の IPsec 機能の報告](reporting-a-nic-s-ipsec-capabilities.md)」を参照してください。

このミニポートは、**サポートさ**れているで1つ以上のフラグを設定することによって、受信 UDP カプセル化 ESP パケットを解析する NIC の機能を報告します。 NDIS\_IPSEC\_オフロード\_V1 構造の**予約**されたメンバー。 ミニポートドライバーでは、 [UDP Esp カプセル](udp-esp-encapsulation-types.md)化の種類で説明されている4つの udp esp カプセル化サブタイプのいずれかまたはすべてを指定できます。

UDP ESP 解析機能を有効または無効にする方法の詳細については、「 [Tcp/ip オフロードサービスの有効化と無効化](enabling-and-disabling-task-offload-services.md)」を参照してください。

 

 





