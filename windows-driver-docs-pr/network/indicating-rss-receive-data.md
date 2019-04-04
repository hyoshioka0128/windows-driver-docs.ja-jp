---
title: データを受信するかを示す RSS
description: データを受信するかを示す RSS
ms.assetid: 8d040d7d-3a8a-4d81-8508-8de225e000ab
keywords:
- 受信側のスケーリング WDK ネットワーク、データの受信を示す
- RSS WDK ネットワーク、データの受信を示す
- WDK RSS データを受信することを示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8178350f17c802aacdc5e274e99dad311a10c8ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531353"
---
# <a name="indicating-rss-receive-data"></a>データを受信するかを示す RSS





ミニポート ドライバーを呼び出すことで受信したデータを示します、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数からその[ *MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)関数。

NIC が正常で RSS ハッシュ値を計算後、ドライバーする必要がありますハッシュ関数、ハッシュの種類を保存し、ハッシュ値で、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体次のマクロ:

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_型**](https://msdn.microsoft.com/library/windows/hardware/ff568409)

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff568408)

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_値**](https://msdn.microsoft.com/library/windows/hardware/ff568410)

ハッシュの種類は、経由でハッシュを計算する必要がある受信パケットの領域を識別します。 ハッシュの種類の詳細については、[RSS ハッシュ型](rss-hashing-types.md)を参照してください。 ハッシュ関数は、ハッシュ値を計算に使用される関数を識別します。 ハッシュ関数の詳細については、[RSS ハッシュ関数](rss-hashing-functions.md)を参照してください。 プロトコル ドライバーでは、ハッシュ型と初期化の時点で関数を選択します。 詳細については、[RSS 構成](rss-configuration.md)を参照してください。

ハッシュの種類を指定ししてはいけないパケットの領域を識別するために、NIC が失敗した場合、計算やスケーリングにハッシュいずれかです。 この場合、ミニポート ドライバーまたは NIC は、既定の CPU に受信したデータを割り当てる必要があります。

受信バッファーがなくなると、NIC 場合、各バッファー返す必要がある、元の受信と DPC を返します。 ミニポート ドライバーが NDIS の状態で、受信したデータを示す\_状態\_リソース。 この場合は、上にあるドライバーは、バッファー記述子のコピーと、すぐに元の所有権を放棄の低速のパスを経由するは。

ネットワーク データの受信についての詳細については、[ネットワーク データの受信](receiving-network-data.md)を参照してください。

 

 





