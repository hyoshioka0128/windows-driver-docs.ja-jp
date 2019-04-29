---
title: RSS および VMQ 受信タスク オフロードでの NVGRE のサポート
description: このセクションでは、NVGRE のサポートについて説明します RSS および VMQ 受信タスク オフロード
ms.assetid: 42660D55-31C0-4101-9EA1-159EBB76B019
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f0bf5311665b7a7a362b314d28ebe698f2c0dc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384217"
---
# <a name="supporting-nvgre-in-rss-and-vmq-receive-task-offloads"></a>RSS および VMQ 受信タスク オフロードでの NVGRE のサポート


NDIS 6.30 (Windows Server 2012) が導入されています[Network Virtualization using Generic Routing Encapsulation (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)します。 NDIS ミニポート ドライバーと Nic を実行する[Receive Side Scaling](receive-scaling.md) (RSS) と[仮想マシン キュー (VMQ)](virtual-machine-queue--vmq-.md)受信タスクのオフロードが方法で NVGRE をサポートするために行う必要があります。

**注**  このページは、内の情報に精通していることを前提としています。 [、セグメント化の大きな TCP パケットのオフロード](offloading-the-segmentation-of-large-tcp-packets.md)します。

 

これらの機能を提供する必要があります、ミニポート ドライバーでは、カプセル化されたパケットの RSS および VMQ をサポートする場合、 **RssSupported**と**VmqSupported**のメンバー、 [ **NDIS\_カプセル化\_パケット\_タスク\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/jj991956)構造体。 ミニポート受信、これらの機能を提供する場合、 [OID\_TCP\_オフロード\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569807) OID 要求し、OID が成功した NIC は、アドバタイズされたで RSS および VMQ を実行する必要がありますカプセル化されたパケットの種類。

解析することができますをカプセル化されたパケットのサポートされている場合、NIC はの内部 MAC ヘッダー、トランスポート (内部) の IP ヘッダーと VMQ のペイロードに TCP または UDP ヘッダーで RSS を実行する必要があります。

」の説明に従って必要があります、NIC をカプセル化されたパケットのトランスポート (内部) の IP ヘッダーを取得するよう RSS および VMQ を実行するため[受信パスでカプセル化パケットをトランスポート ヘッダーを検索する](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)プロトコル番号を確認します。 NIC は、NIC を解析できるプロトコルを使用するパケットを受信する場合は、NIC が必要です。

-   トランスポート (内部) の IP ヘッダーと TCP または UDP ヘッダーで 4 タプル ハッシュを実行して、RSS を実行します。
    -   カプセル化されたパケットのプロトコルのミニポートを解析できません、NIC がトンネル (外部) の IP ヘッダーの元とコピー先のアドレス フィールドに 2 タプル ハッシュを実行する必要があります。
    -   トランスポート (内部) の IP ヘッダーの直後、TCP または UDP ヘッダーを含まないカプセル化されたパケット、NIC がトンネル (外部) の IP ヘッダーの元とコピー先のアドレス フィールドに 2 タプル ハッシュを実行する必要があります。
-   VMQ を実行するには、カプセル化されたパケットでイーサネット ヘッダーを使用します。 (内のカプセル化されたパケット)、イーサネット ヘッダーを含まないカプセル化されたパケット、最も外側にあるイーサネット ヘッダーを使用して VMQ を実行する必要があります。

 

 





