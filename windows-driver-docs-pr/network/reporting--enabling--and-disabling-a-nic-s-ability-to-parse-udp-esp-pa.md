---
title: レポート機能を有効にする、および UDP ESP パケットを解析する NIC の機能を無効にします。
description: レポート機能を有効にする、および UDP ESP パケットを解析する NIC の機能を無効にします。
ms.assetid: 3a75c5b2-2d94-428e-9b2a-d760e14df552
keywords:
- WDK の IPsec ESP パケットを UDP カプセル化オフロード、機能の解析
- WDK IPsec オフロード機能を解析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a46badf0be2c795728d9311e257cea5097e4994
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373286"
---
# <a name="reporting-enabling-and-disabling-a-nics-ability-to-parse-udp-esp-packets"></a>レポート機能を有効にする、および UDP ESP パケットを解析する NIC の機能を無効にします。

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




ミニポート ドライバーでの NIC のインターネット プロトコル セキュリティ (IPsec) 機能を指定します、 [ **NDIS\_IPSEC\_オフロード\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)構造体。 詳細については、次を参照してください。 [NIC の IPsec 機能を Reporting](reporting-a-nic-s-ipsec-capabilities.md)します。

ミニポート 1 つまたは複数のフラグを設定して受信 ESP の UDP カプセル化パケットを解析する NIC の機能の報告、**サポートされている**します。 **予約済み**の NDIS メンバー\_IPSEC\_オフロード\_V1 構造体。 ミニポート ドライバーが記載されている 4 つの UDP ESP カプセル化のサブタイプの一部またはすべてを指定できます[UDP ESP カプセル化型](udp-esp-encapsulation-types.md)します。

有効化と disableing UDP ESP の解析機能については、次を参照してください。[の有効化と無効にすると TCP/IP のオフロード サービス](enabling-and-disabling-task-offload-services.md)します。

 

 





