---
title: データ チャネルの特性
description: データ チャネルの特性
ms.assetid: 3e178d82-32de-468c-8175-4b0c2684be76
keywords:
- 一括 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa88c38ed4c0c2ad4dcbe6f12951df8196d42d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362329"
---
# <a name="data-channel-characteristics"></a>データ チャネルの特性





デバイスのデータ チャネルから成る、*一括*IN および OUT エンドポイント、*データ クラス*インターフェイス。

どちらの方向に 1 つの USB データ転送は、1 つので構成される[リモート\_NDIS\_パケット\_MSG](remote-ndis-packet-msg.md)または長い multipacket メッセージ。

ホストからデバイスへのデータ メッセージを送信する USB 転送は、データ クラス インターフェイスの一括 OUT エンドポイントへの標準的な USB 一括転送します。

デバイスからホストにデータ メッセージを送信する USB 転送は、データ クラス インターフェイスの一括でエンドポイントからの標準的な USB 一括転送します。 ホストはによって示されるバイト数の最大読み取りは、 *MaxTransferSize*フィールド[リモート\_NDIS\_初期化\_MSG](remote-ndis-initialize-msg.md)より小さくなります。USB 1.1 デバイスの 0x4000 バイト数。

 

 





