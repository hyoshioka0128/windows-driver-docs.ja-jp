---
title: NDIS 電源管理の概要
description: NDIS 電源管理の概要
ms.assetid: 8ae3803f-c3e4-4499-9e61-678f4ab61fbc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e0cfd9044fbf8d6a5369a2ea40b3d77380ffa9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378281"
---
# <a name="ndis-power-management-overview"></a>NDIS 電源管理の概要





このセクションでは、NDIS 6.20 ドライバーを Windows 7 で導入される電源管理インターフェイスで提供される機能の概要を示します。

ミニポート ドライバーおよび NDIS 6.20 が動作し、以降のバージョンの NDIS をサポートするプロトコル ドライバーには、NDIS 6.20 が動作電源管理インターフェイスをサポートする必要があります。 ただし、NDIS は、古いネットワーク アダプターと NDIS 6.1 または NDIS 6.20 が動作の電源管理機能をサポートしていない以前のミニポート ドライバーの以前のインターフェイスへの変換を提供します。 NDIS 6.20 旧バージョンとの互換性の問題に関する詳細については、次を参照してください。 [NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)します。

NDIS 6.20 電源管理のインターフェイスをサポートします。

-   パケットに基づく wake on LAN (WOL) パターンは、NDIS 6.1 と従来の手法をさらに入力します。 そのため、NDIS 6.20 WOL パターンはウェイク アップの不要なイベントを回避するためより特定できます。 たとえば、ネットワーク アダプターは TCP を識別できます (SYN) のパケットを同期します。 WOL 方法の詳細については、次を参照してください。 [NDIS 6.20 WOL メソッド](wol-methods-in-ndis-6-20.md)します。

-   プロトコルは、最も一般的なプロトコルの一部のネットワーク アダプターにオフロードします。 プロトコルは、ネットワーク アダプターにオフロードは、ため、ウェイク アップの不要なイベントを回避するためにコンピューターに代わって応答できます。 たとえば、ネットワーク アダプターでは、コンピューターのスリープ解除なく IPv4 アドレス解決プロトコル (ARP) と IPv6 近隣要請 (NS) プロトコル パケットを処理できます。 電源管理プロトコルの詳細については、オフロードを参照してください[プロトコルの NDIS 電源管理の負荷を軽減](protocol-offloads-for-ndis-power-management.md)します。

NDIS を使用して低電力状態を設定し、全機能を復元する一連の WOL イベントについては、次を参照してください。 [Wake on LAN の低電力](low-power-for-wake-on-lan.md)します。

NDIS 6.20 が動作の電源管理もサポートしています。

-   NDIS 6.20 が動作は、メディアが接続したときにネットワーク アダプターを電力状態に戻すことができます。 オペレーティング システムでは、メディアが切断されている場合に、低電力状態でネットワーク アダプターを書き込みます。 メディアが切断されたときに、低電力状態を設定する方法についての詳細については、次を参照してください。[メディア切断の低電力](low-power-on-media-disconnect.md)します。

ここでは、次のトピックについて説明します。

[NDIS 6.20 WOL メソッド](wol-methods-in-ndis-6-20.md)

[電源管理の NDIS WOL パターン](wol-patterns-for-ndis-power-management.md)

[NDIS 電源管理のためのプロトコルのオフロード](protocol-offloads-for-ndis-power-management.md)

 

 





