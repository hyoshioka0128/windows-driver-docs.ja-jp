---
title: WAN パケットフレーミングの概要
description: WAN パケットフレーミングの概要
ms.assetid: 11a6fbf5-c7a9-474b-811e-c77a36e834f3
keywords:
- WAN ミニポートドライバー WDK ネットワーク、パケット
- CoNDIS WAN ドライバー WDK ネットワーク、パケット
- パケットフレーミング WDK WAN
- NDISWAN WDK ネットワーク
- WAN パケットフレーミング WDK ネットワーク
- パケットフレーミング WDK WAN、WAN パケットフレームについて
- Wan パケットフレーミング WDK ネットワーク、WAN パケットフレームについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33b1490e986bd03a1a8a33eb2e5581458a332aad
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565625"
---
# <a name="wan-packet-framing-overview"></a>WAN パケットフレーミングの概要





ここでは、WAN パケットフレーミングについて説明します。

NDISWAN 中間ドライバーは、wan ミニポートドライバーによって実行される wan パケットフレームに関する情報を、 [OID\_wan\_\_MEDIUM サブタイプ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))クエリ情報に対するミニポートドライバーの応答から取得します。申請.

NDISWAN は、パケットを LAN から PPP 形式に変換します。 NDISWAN は、単純な HDLC フレームを使用します。 メディア固有のフレームの大部分は、ミニポートドライバーによって実行される必要があります。

WAN ミニポートドライバーの send 関数にパケットを送信する前に、NDISWAN は単純な PPP HDLC フレーミングを行います。 単純な PPP HDLC フレームは、FC、ビットまたはバイトの手紙、および開始または終了フラグのない PPP の HDLC です。

次のトピックでは、WAN パケットフレーミングに関する追加情報を提供します。

[非同期フレーム](asynchronous-framing.md)

[ISDN とスイッチ-56K フレーム](isdn-and-switched-56k-framing.md)

 

 





