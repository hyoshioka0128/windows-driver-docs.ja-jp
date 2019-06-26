---
title: WDI 拡張チャネル スイッチ アナウンス (ECSA)
description: このセクションでは、拡張チャネル スイッチのお知らせ (ECSA) を実装するために推奨されるドライバーとファームウェアの変更を提供します。
ms.assetid: 9C59C8A2-335F-4BA4-8682-6DFFB82E1CAF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aea45a28acbb098ba0204b849c2dcbf5e62b27f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384339"
---
# <a name="wdi-extended-channel-switch-announcement-ecsa"></a>WDI 拡張チャネル スイッチ アナウンス (ECSA)


モードでは、大文字と小文字が 1 つのチャネルとして望めませんマルチ チャネルの使用のユース ケースを最小限に抑える、Wi-Fi Direct ポートによって、マルチ チャネルで動作するシステム場合。 (ドライバーとファームウェア) デバイスが ECSA を実装することをお勧めします。 この機能は、IHV 側で完全に存在する必要があります。

推奨されるドライバーとファームウェアの変更を次に示します。

-   Wi-Fi Direct のポートで双方向 ECSA をサポートします。
-   デバイス グループの所有者でマルチ チャネルのモードでは。
    -   リモート ピアが ECSA をサポートしているかどうか、ドライバーが検出する必要があります。
    -   リモート ピアに ECSA がサポートしている場合は、ピアを 1 つのチャネルを生成するチャネルの構成に移動する ECSA に情報交換できます。
-   デバイスは、クライアントでマルチ チャネルのモードでは。
    -   ECSA 要求をリモート ピアからの場合、サポートします。
-   オペレーティング システムにチャネルの変更通知を送信[NDIS\_状態\_WDI\_INDICATION\_P2P\_グループ\_オペレーティング\_チャネル](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-p2p-group-operating-channel).

 

 





