---
title: ネットワーク ドライバーのプログラミングに関する考慮事項
description: ネットワーク ドライバーのプログラミングに関する考慮事項
ms.assetid: 43e97f33-8470-440c-b4f4-78752def2dcf
keywords:
- ネットワーク ドライバー WDK、プログラミングの考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc4226ba0cc1db8c5e69397a47b2e082d843aa0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365740"
---
# <a name="network-driver-programming-considerations"></a>ネットワーク ドライバーのプログラミングに関する考慮事項





Microsoft Windows ネットワーク ドライバーは、同様の設計目標を共有します。 移植性とスケーラビリティ、ハードウェアとソフトウェア、オブジェクト ベースのインターフェイスを使用し、非同期 I/O をサポートするための単純な構成を提供する、ネットワーク ドライバーが書き込まれます。 このセクションでは、Microsoft Windows Vista およびそれ以降のオペレーティング システム用に作成したネットワーク ドライバーをこれらの一般的な設計目標を適用する方法について説明します。

ここでは、次のトピックについて説明します。

-   [ネットワークのドライバーでのパフォーマンス](performance-in-network-drivers.md)
-   [ネットワーク アダプターのパフォーマンス](performance-in-network-adapters.md)
-   [ネットワークのドライバーでの移植性](portability-in-network-drivers.md)
-   [ネットワークのドライバーでマルチプロセッサ サポート](multiprocessor-support-in-network-drivers.md)
-   [ネットワークのドライバーの Irql](irqls-in-network-drivers.md)
-   [同期とネットワーク ドライバーでの通知](synchronization-and-notification-in-network-drivers.md)
-   [ネットワークのドライバーでのパケット構造](packet-structures-in-network-drivers.md)
-   [共有ネットワーク ドライバーのメモリを使用](using-shared-memory-in-network-drivers.md)
-   [非同期 I/O とネットワーク ドライバーでの入力候補関数](asynchronous-i-o-and-completion-functions-in-network-drivers.md)
-   [ネットワークのドライバーに関するセキュリティの問題](security-issues-for-network-drivers.md)

 

 





