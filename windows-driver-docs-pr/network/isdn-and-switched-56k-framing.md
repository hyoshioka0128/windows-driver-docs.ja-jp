---
title: ISDN およびスイッチド 56K フレーミング
description: ISDN およびスイッチド 56K フレーミング
ms.assetid: e0532ded-c429-4f3a-b3c9-fd8ccc6b1b65
keywords:
- パケットのフレーミングの WDK WAN、ISDN フレーム
- ISDN WDK WAN のフレーム化
- パケットのフレーミング WDK WAN 56 K のフレームの切り替え
- WDK WAN フレーム スイッチの 56 K
- WAN パケットのフレーミング WDK ネットワー キング、ISDN フレーム
- WAN のパケットがネットワーク、スイッチのフレーム化 56 K WDK のフレーム化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3bf24405b5c50b20f7fd91d8231f4dc95974094
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353772"
---
# <a name="isdn-and-switched-56k-framing"></a>ISDN およびスイッチド 56K フレーミング





最初に、ISDN B チャネル (D チャネルではない) を使用する必要があります。 B の複数のチャネルのサポートは NDISWAN のマルチリンク サポートを通じて行われます。 最初に、NRZ エンコード付きのビット同期 HDLC フレームを使用する必要があります。 ドライバーや ISDN ハードウェアによっては、透明度を指定する必要があります。 また、ISDN ドライバーまたは NRZ PPP 終了フラグ (0x7E) を追加して、任意の時間の間のフレームの塗りつぶしを挿入する FCS を計算する、エンコーディングを提供するハードウェアの役割です。 交換 56 K ドライバーは、ISDN と同じ方法でフレームする必要があります。

 

 





