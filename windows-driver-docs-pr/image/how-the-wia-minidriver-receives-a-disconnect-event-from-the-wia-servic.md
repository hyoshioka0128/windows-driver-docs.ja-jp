---
title: Wia ミニドライバーが WIA から切断を受け取る方法
description: Wia ミニドライバーが WIA サービスから切断イベントを受信する方法
ms.assetid: 6ae3c230-d026-469e-a699-860a295fba85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056c06ffdf18b9387d9f2b33de239b1df3b8a1f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840830"
---
# <a name="how-the-wia-minidriver-receives-a-disconnect-event-from-the-wia-service"></a>Wia ミニドライバーが WIA サービスから切断イベントを受信する方法

ユーザーがコンピューターから USB ケーブルを切断したときなど、デバイスがコンピューターから突然切断された場合、WIA サービスは、WIA\_イベント\_デバイスを使用して[**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドを呼び出し\_切断されたイベント。 **IWiaMiniDrv::D rvnotifypnpevent**メソッドの実装例については、「[割り込みイベントのサポートの追加](adding-interrupt-event-support.md)」を参照してください。

このイベントの発生中または後に、WIA ミニドライバーはハードウェアとの通信を試行しないでください。 このイベントは、WIA サービスによってミニドライバーがアンロードされることを示します。 次に許可されるデバイスアクセスは、WIA サービスがミニドライバーを再読み込みするときです。 ミニドライバーは、再接続されるまで、すべての[IWiaMiniDrv](iwiaminidrv-com-interface.md)インターフェイス呼び出しがハードウェアにアクセスするのを防ぐフラグを設定することをお勧めします。

WIA\_イベント\_デバイス\_切断イベントは、常に WIA ミニドライバーに送信されるとは限りません。 コンピューターがシャットダウンしているときに、WIA サービスが WIA ドライバーをアンロードしている場合、このイベントは送信されません。 このイベントは、デバイスのハードウェアを無効にするアクションとして扱う必要があります。

 



