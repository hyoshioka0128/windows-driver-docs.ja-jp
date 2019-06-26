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
ms.openlocfilehash: 8cf715f3f76d2a8a89296fe3c836bb3b16acbc9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385522"
---
# <a name="indicating-rss-receive-data"></a>RSS 受信データの表示





ミニポート ドライバーを呼び出すことで受信したデータを示します、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数からその[ *MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)関数。

NIC が正常で RSS ハッシュ値を計算後、ドライバーする必要がありますハッシュ関数、ハッシュの種類を保存し、ハッシュ値で、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体次のマクロ:

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_型**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-type)

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_関数**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-function)

[**NET\_バッファー\_一覧\_設定\_ハッシュ\_値**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-value)

ハッシュの種類は、経由でハッシュを計算する必要がある受信パケットの領域を識別します。 ハッシュの種類の詳細については、次を参照してください。 [RSS ハッシュ型](rss-hashing-types.md)します。 ハッシュ関数は、ハッシュ値を計算に使用される関数を識別します。 ハッシュ関数の詳細については、次を参照してください。 [RSS ハッシュ関数](rss-hashing-functions.md)します。 プロトコル ドライバーでは、ハッシュ型と初期化の時点で関数を選択します。 詳細については、次を参照してください。 [RSS 構成](rss-configuration.md)します。

ハッシュの種類を指定ししてはいけないパケットの領域を識別するために、NIC が失敗した場合、計算やスケーリングにハッシュいずれかです。 この場合、ミニポート ドライバーまたは NIC は、既定の CPU に受信したデータを割り当てる必要があります。

受信バッファーがなくなると、NIC 場合、各バッファー返す必要がある、元の受信と DPC を返します。 ミニポート ドライバーが NDIS の状態で、受信したデータを示す\_状態\_リソース。 この場合は、上にあるドライバーは、バッファー記述子のコピーと、すぐに元の所有権を放棄の低速のパスを経由するは。

ネットワーク データの受信についての詳細については、次を参照してください。[ネットワーク データの受信](receiving-network-data.md)します。

 

 





