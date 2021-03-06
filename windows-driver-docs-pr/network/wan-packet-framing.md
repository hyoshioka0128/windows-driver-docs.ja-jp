---
title: WAN パケット フレーミング
description: WAN パケット フレーミング
ms.assetid: 11a6fbf5-c7a9-474b-811e-c77a36e834f3
keywords:
- WAN ミニポート ドライバー WDK ネットワー キング、パケット
- ドライバー WDK ネットワーク、WAN いる CoNDIS パケット
- パケットのフレーミング WDK WAN
- ネットワーク NDISWAN WDK
- WAN のパケットのフレーミング WDK ネットワーク
- WAN のパケットのフレーミングの WDK WAN のフレーム化パケット
- WAN パケットのフレーミング WDK ネットワーク、WAN パケットのフレーミングについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b47073f18d34134dab135939bab30f46d7fc81ff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384349"
---
# <a name="wan-packet-framing"></a>WAN パケット フレーミング





このセクションでは、WAN パケットのフレーミングについての情報を提供します。

NDISWAN 中間ドライバーに、ミニポート ドライバーの応答から WAN ミニポート ドライバーによって実行される WAN パケット フレームに関する情報を取得する、 [OID\_WAN\_MEDIUM\_サブタイプ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))クエリ情報の要求。

NDISWAN は、LAN から、発信パケット PPP 形式に変換します。 NDISWAN では、単純な HDLC フレームを使用します。 ミニポート ドライバーでは、メディア固有のフレームの大部分を実行する必要があります。

WAN ミニポート ドライバーの送信機能にパケットを送信する前に、NDISWAN は、単純な HDLC の PPP フレームを行います。 単純な HDLC の PPP フレームは、PPP の HDLC のフレーミング、FC、ビットやバイト作業を手伝えば、先頭または末尾フラグのいずれかです。

次のトピックでは、WAN のパケットのフレーミングに関する追加情報を提供します。

[非同期フレーム](asynchronous-framing.md)

[ISDN および交換 56 K フレーム](isdn-and-switched-56k-framing.md)

 

 





