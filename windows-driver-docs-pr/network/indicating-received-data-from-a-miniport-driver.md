---
title: ミニポート ドライバーからの受信データの表示
description: ミニポート ドライバーからの受信データの表示
ms.assetid: da5d31e9-5212-4c6c-bac2-81432a46c303
keywords:
- 受信側のデータの WDK ネットワーク
- NdisMIndicateReceiveNetBufferLists
- indicatings WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 275fe244009dada90a2848ad8faee1ac5e680bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327794"
---
# <a name="indicating-received-data-from-a-miniport-driver"></a>ミニポート ドライバーからの受信データの表示





次の図に、ミニポート ドライバーを示す値を受信します。

![通知のミニポート ドライバーを示す図](images/miniportreceive.png)

ミニポート ドライバーの呼び出し、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)をネットワークからのデータの受信を示す関数。 **NdisMIndicateReceiveNetBufferLists**関数の指定された一覧を渡します[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体にスタックをセットアップします。上にあるドライバー。

ミニポート ドライバーが設定されている場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)、ミニポート ドライバーでの所有権を取り戻す必要があることを示します、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)すぐに構造体します。 この場合は、NDIS 呼び出しませんミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)を返す関数、 **NET\_バッファー\_一覧**構造体。 ミニポート ドライバーが所有権を得た直後後**NdisMIndicateReceiveNetBufferLists**を返します。

ミニポート ドライバーが設定されていない場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)、NDIS を返します、指定された[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造をミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)関数。 ミニポート ドライバーが指定された構造体の所有権を解放する NDIS が返す順序にするまでこの場合、 *MiniportReturnNetBufferLists*します。

 

 





