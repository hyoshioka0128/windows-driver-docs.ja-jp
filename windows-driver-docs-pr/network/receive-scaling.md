---
title: Receive Side Scaling のサポート
description: Receive Side Scaling のサポート
ms.assetid: db0d8178-ae6c-4513-9c8c-f10615d1bbce
keywords:
- スケーラブルなネットワーク WDK
- 受信側のスケーリング WDK ネットワーク
- RSS の WDK ネットワーク
- ミニポート ドライバー WDK ネットワークは、受信パケットの処理のスケーリング
- NDIS ミニポート ドライバー WDK、受信パケットの処理のスケーリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7dfbc32f26760f9febe475b0ecd52067a122e9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372217"
---
# <a name="receive-side-scaling-support"></a>Receive Side Scaling のサポート





NDIS 6.0 には、受信パケットの複数のプロセッサの処理のスケーリングのサポートが導入されました。 受信側 scaling (RSS) インターフェイスには、複数 NIC のハードウェア サポートのレベルが対応しています。

受信したデータに関連付けるターゲット プロセッサは、現在の RSS の構成に基づいて、ミニポート ドライバーまたは NIC から決定します。 使用可能なターゲットのプロセッサの最も効率的に使用する RSS の構成を調整できます。

ミニポート ドライバーまたは NIC は、ターゲットのプロセッサに関連付けられている受信キューに受信したデータを割り当てます。 遅延プロシージャ呼び出し (Dpc) の空のターゲット プロセッサをスケジュールする NDIS ミニポート ドライバー要求キューが表示されます。

NDIS は、各ターゲットの指定されたプロセッサの DPC をスケジュールします。 各 DPC は、指定されたターゲットのプロセッサ上の特定の受信キューを処理します。

NDIS 6.0 の詳細については、受信側のスケーリングを参照してください[Receive Side Scaling](ndis-receive-side-scaling2.md)します。

 

 





