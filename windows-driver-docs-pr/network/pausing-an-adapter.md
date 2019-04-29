---
title: アダプターの一時停止
description: アダプターの一時停止
ms.assetid: e24a9886-a1d7-4ca5-bed8-85db4a49ed9c
keywords:
- ミニポート アダプタ WDK ネットワーク、一時停止
- アダプター WDK ネットワーク、一時停止
- 一時停止状態の WDK ネットワーク
- WDK のネットワークを一時停止の状態
- MiniportPause
- ミニポート アダプターが一時停止
- ミニポート アダプターが停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4316b3e0eaaeaa7dca4c9b8552b1dec49d519556
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385012"
---
# <a name="pausing-an-adapter"></a>アダプターの一時停止





NDIS ミニポート ドライバーを呼び出す[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)一時停止操作を開始する関数。 アダプターは、一時停止操作が完了するまで一時停止状態のままです。

一時停止状態では、ミニポート ドライバーを未処理に完了する必要がありますの操作を受信します。 ドライバーでは、未処理の送信操作を完了する必要がありますも、新しい送信要求を拒否する必要があります。

完了する受信操作を行うすべての呼び出しに、ドライバーが待機する、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)を返す関数と NDIS は未処理のすべてに返す必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体、ミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)関数。

未処理の送信操作を完了するミニポート ドライバーを呼び出す必要があります、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数のすべての未処理の NET\_バッファー\_リストの構造体。 ドライバーに対して行われたすべての新しい送信要求を拒否すべきその[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)すぐに機能します。

ミニポート ドライバーでは、未処理のすべての送信が完了するし、受信操作、ドライバーは、同期または非同期で一時停止要求を完了する必要があります。 ドライバーを呼び出す場合は、一時停止操作が非同期的に完了したら、 [ **NdisMPauseComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563628)一時停止要求を完了します。 一時停止要求を完了すると、ミニポート ドライバーが一時停止状態です。

NDIS はいない停止など、他のプラグ アンド プレイ操作を開始、初期化、電源変更、または再起動操作、ミニポート ドライバーが一時停止中の状態。 NDIS は、ミニポート ドライバーは一時停止状態になった後、これらのプラグ アンド プレイ操作を開始できます。

 

 





