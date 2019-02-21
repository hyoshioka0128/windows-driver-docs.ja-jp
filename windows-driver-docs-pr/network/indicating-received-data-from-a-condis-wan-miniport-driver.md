---
title: いる CoNDIS WAN ミニポート ドライバーからデータを受信したことを示します
description: いる CoNDIS WAN ミニポート ドライバーからデータを受信したことを示します
ms.assetid: d49ea741-df5c-4b65-b899-a751cb2b9929
keywords:
- データを受信している CoNDIS WAN のドライバー WDK ネットワーク
- 受信側のデータの WDK ネットワーク
- WDK いる CoNDIS WAN の問題
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b2babe8e7ddde0ac5739a2352af8e318670a47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552858"
---
# <a name="indicating-received-data-from-a-condis-wan-miniport-driver"></a>いる CoNDIS WAN ミニポート ドライバーからデータを受信したことを示します





次の操作は、いる CoNDIS WAN ミニポート ドライバー ネットワーク データ パケットを受信するときに発生します。

1.  ドライバーは、呼び出す前に必要な場合、ネットワーク データ パケットからドライバー固有のカプセル化を削除[ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561) NETで受信したデータを示す\_バッファー\_リスト構造体。 たとえば、ドライバーは、PPPoE カプセル化を削除できます。 ただし、ミニポート ドライバーままようになど、PPP ヘッダーとペイロードのカプセル化されたデータ。

2.  ドライバーの呼び出し、 **NdisMCoIndicateReceiveNetBufferLists** NDISWAN にパケットが届いたことを示す関数。

3.  パケットと呼び出しを処理する NDISWAN [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)をパケットの到着を示すためにします。

4.  パケット、NDIS 呼び出しを転送するように、 [ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)上にあるバインドのプロトコル ドライバーの関数。

 

 





