---
title: RSS 受信データの表示
description: RSS 受信データの表示
ms.assetid: 8d040d7d-3a8a-4d81-8508-8de225e000ab
keywords:
- 受信側のスケーリング WDK ネットワーク、データの受信を示す
- RSS WDK ネットワーク、データの受信を示す
- WDK RSS データを受信することを示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8178350f17c802aacdc5e274e99dad311a10c8ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327723"
---
# <a name="indicating-rss-receive-data"></a>RSS 受信データの表示





ミニポート ドライバーを呼び出すことで受信したデータを示します、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数からその[ *MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)関数。

NIC が正常で RSS ハッシュ値を計算後、ドライバーする必要がありますハッシュ関数、ハッシュの種類を保存し、ハッシュ値で、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体次のマクロ:

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_型**](https://msdn.microsoft.com/library/windows/hardware/ff568409)

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff568408)

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_値**](https://msdn.microsoft.com/library/windows/hardware/ff568410)

ハッシュの種類は、経由でハッシュを計算する必要がある受信パケットの領域を識別します。 ハッシュの種類の詳細については、次を参照してください。 [RSS ハッシュ型](rss-hashing-types.md)します。 ハッシュ関数は、ハッシュ値を計算に使用される関数を識別します。 ハッシュ関数の詳細については、次を参照してください。 [RSS ハッシュ関数](rss-hashing-functions.md)します。 プロトコル ドライバーでは、ハッシュ型と初期化の時点で関数を選択します。 詳細については、次を参照してください。 [RSS 構成](rss-configuration.md)します。

ハッシュの種類を指定ししてはいけないパケットの領域を識別するために、NIC が失敗した場合、計算やスケーリングにハッシュいずれかです。 この場合、ミニポート ドライバーまたは NIC は、既定の CPU に受信したデータを割り当てる必要があります。

受信バッファーがなくなると、NIC 場合、各バッファー返す必要がある、元の受信と DPC を返します。 ミニポート ドライバーが NDIS の状態で、受信したデータを示す\_状態\_リソース。 この場合は、上にあるドライバーは、バッファー記述子のコピーと、すぐに元の所有権を放棄の低速のパスを経由するは。

ネットワーク データの受信についての詳細については、次を参照してください。[ネットワーク データの受信](receiving-network-data.md)します。

 

 





