---
title: CoNDIS でのデータの送信と受信
description: CoNDIS でのデータの送信と受信
ms.assetid: aad7ccf9-0eaa-4327-b048-268d12593a70
keywords:
- WDK いる CoNDIS 仮想接続は、データを転送します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242b9228d72472cd2d07fe18b8f2141c21fc64a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366258"
---
# <a name="sending-and-receiving-data-in-condis"></a>CoNDIS でのデータの送信と受信





データを転送するには、パケットを定評のある、アクティブ化された VC 経由で送受信する必要があります。

**注**  プロトコル ドライバーを呼び出してはならない[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728) VC を呼び出した後にデータを送信する[ **NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627)その VC の。

 

関数の送受信をいる CoNDIS はコネクションレスの送信に似ており、受信機能。 いる CoNDIS とコネクションレス インターフェイスの主な違いは、仮想接続 (VCs) の管理です。 コネクションレス型の詳細については送信し受信操作を参照してください[送信および受信操作](send-and-receive-operations.md)します。

1 つの関数の呼び出し、いる CoNDIS ドライバーが複数送信できます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)複数構造[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造で各 NET\_バッファー\_リスト構造体。 また、NET の複数の操作の送信いる CoNDIS ドライバーを示す完了\_バッファー\_リスト構造で複数の NET\_各ネットワーク上のバッファーの構造体\_バッファー\_リスト構造。

受信パスでいる CoNDIS ミニポート ドライバーが NET の一覧を指定できます\_バッファー\_を示すために、リストの構造体を受け取ります。 各ネット\_バッファー\_ミニポート ドライバーを提供するリストには、1 つのネットワークが含まれています。\_バッファーの構造体。 別のプロトコル バインディングは、各ネットワークを処理できるため、\_バッファー\_リスト構造では、NDIS が各 NET を個別に返すことできます\_バッファー\_ミニポート ドライバーにリストの構造体。

NDIS 5 をサポートします。*x*し以前ドライバーは、従来の間で変換レイヤーを提供している CoNDIS [ **NDIS\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff557086)構造と、NET\_バッファー ベース構造体。 NET の間で、必要な変換を実行している CoNDIS\_バッファーの構造と NDIS\_パケットの構造体。 翻訳のためのパフォーマンスを低下させることを回避するには、NET のサポートにいる CoNDIS ドライバーを更新\_構造体をバッファーし、複数のネットワークをサポートする必要があります\_バッファー\_すべてのデータ パスのリストの構造体。

ここでは、次のトピックについて説明します。

[NET の送信\_いる CoNDIS ドライバーからのバッファーの構造体](sending-net-buffer-structures-from-condis-drivers.md)

[NET の受信\_いる CoNDIS ドライバーにバッファーの構造体](receiving-net-buffer-structures-in-condis-drivers.md)

 

 





