---
title: RSS および VMQ 受信タスク オフロードでの NVGRE のサポート
description: このセクションでは、RSS および VMQ 受信タスクのオフロードでの NVGRE のサポートについて説明します。
ms.assetid: 42660D55-31C0-4101-9EA1-159EBB76B019
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd2f3a9f274b1c06785dff637a3c2f2f71f23f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841791"
---
# <a name="supporting-nvgre-in-rss-and-vmq-receive-task-offloads"></a>RSS および VMQ 受信タスク オフロードでの NVGRE のサポート


NDIS 6.30 (Windows Server 2012) では、[汎用ルーティングカプセル化 (NVGRE) を使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)が導入されています。 [Receive Side Scaling](receive-scaling.md) (RSS) と[仮想マシンキュー (VMQ)](virtual-machine-queue--vmq-.md)の受信タスクを実行する NDIS ミニポートドライバーと NIC では、nvgre をサポートするようにオフロードする必要があります。

**注**  このページでは、[サイズの大きい TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)に関する情報について理解していることを前提としています。

 

ミニポートドライバーでカプセル化されたパケットの RSS および VMQ がサポートされている場合 、 [**NDIS\_\_パケット\_タスクをカプセル化して、それらの機能をアドバタイズする必要があり\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)構造。 ミニポートがこれらの機能を提供し、oid [\_TCP\_オフロード\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters) oid 要求、および oid に成功した場合、NIC は、アドバタイズされたカプセル化されたパケットの種類で RSS と VMQ を実行する必要があります。

解析可能なサポートされているカプセル化パケットの場合、NIC は、内部 MAC ヘッダーのトランスポート (内部) IP ヘッダーおよび VMQ のペイロードで、TCP または UDP ヘッダーで RSS を実行する必要があります。

RSS と VMQ を実行する場合、NIC はカプセル化されたパケットのトランスポート (内部) IP ヘッダーにアクセスする必要があります。詳細について[は、「受信パスにカプセル化されたパケットのトランスポートヘッダーを配置](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)し、プロトコル番号を確認する」を参照してください。 Nic が解析可能なプロトコルを使用するパケットを受信した場合、nic は次のことを行う必要があります。

-   トランスポート (内部) IP ヘッダーと TCP または UDP ヘッダーに対して4組のハッシュを実行して、RSS を実行します。
    -   ミニポートで解析できないプロトコルを持つカプセル化されたパケットの場合、NIC はトンネル (外部) IP ヘッダーの送信元と送信先のアドレスフィールドに2タプルのハッシュを実行する必要があります。
    -   トランスポート (内部) IP ヘッダーの直後に TCP または UDP ヘッダーが含まれていないカプセル化されたパケットの場合、NIC はトンネル (外部) IP ヘッダーの送信元と送信先のアドレスフィールドに2タプルのハッシュを実行する必要があります。
-   カプセル化されたパケットでイーサネットヘッダーを使用して VMQ を実行します。 カプセル化されたパケット内にイーサネットヘッダーが含まれていないカプセル化されたパケットの場合は、最も外側のイーサネットヘッダーを使用して VMQ を実行する必要があります。

 

 





