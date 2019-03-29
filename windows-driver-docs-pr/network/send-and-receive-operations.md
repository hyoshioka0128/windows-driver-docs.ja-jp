---
title: 送信および受信操作
description: 送信および受信操作
ms.assetid: 216bfed2-92f8-4480-95fc-9909d7c1f533
keywords:
- ネットワーク、WDK のデータを送信します。
- ネットワーク データ、WDK の受信
- WDK のデータ ネットワーク、送信します。
- WDK のデータ ネットワークの受信
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
- NET_BUFFER_LIST
- 複数の NET_BUFFER_LIST 構造 WDK networki
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2652409e479fd2e1823754011352af8cbd9ef049
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579420"
---
# <a name="send-and-receive-operations"></a>送信および受信操作





1 つの関数呼び出しでは、NDIS 6.0 のドライバーが複数送信できます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)複数構造[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造で各 NET\_バッファー\_リスト構造体。 また、NDIS ドライバーが複数のネットワークに完了した送信操作を示すことができます\_バッファー\_リスト構造で複数の NET\_、ネットワーク上のバッファーの構造体\_バッファー\_リスト構造体。

受信パスでは、ミニポート ドライバーが NET のリストを使用できます\_バッファー\_を示すために、リストの構造体を受け取ります。 各ネット\_バッファー\_ミニポート ドライバーによって示されるリストには、1 つのネットワークが含まれています。\_バッファーの構造体。 ただし、ネイティブの 802.11 ドライバーが 1 つ以上のネットワークを持つことができます\_バッファーの構造体。 別のプロトコル バインディングは、各ネットワークを処理できるため、\_バッファー\_リスト構造では、NDIS は、各ネットワークを返すことができます\_バッファー\_ミニポート ドライバーに構造を個別に一覧表示します。

NDIS 5 をサポートします。*x*し、以前のドライバーの間の変換レイヤーを提供する NDIS、 [ **NDIS\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff557086)-ベースと NET\_バッファー ベースのインターフェイス。 NDIS との間、必要な変換を実行する[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造および NDIS\_パケットの構造体。 翻訳によってパフォーマンスの低下を回避するには、NET を使用する NDIS ドライバーを更新\_構造体をバッファーし、複数をサポートする必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)すべてのデータ パス内の構造体。

ここでは、次のトピックについて説明します。

[ネットワーク データを送信します。](sending-network-data.md)

[送信操作のキャンセル](canceling-a-send-operation.md)

[ネットワーク データの受信](receiving-network-data.md)

[ループ バック NDIS パケット](looping-back-ndis-packets.md)

 

 





