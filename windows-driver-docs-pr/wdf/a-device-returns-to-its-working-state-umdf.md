---
title: デバイスが動作状態に戻ります (UMDF 1)
description: デバイスが動作状態に戻る
ms.assetid: 2b192eea-f731-4d61-be19-95724bf7b04a
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスが動作状態に戻る
- デバイスが動作状態に戻ります。 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57331ee75ec73856042555e1980029d13523180b
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141253"
---
# <a name="a-device-returns-to-its-working-state-umdf-1"></a>デバイスが動作状態に戻ります (UMDF 1)


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次のいずれかが発生した場合、低電力状態のデバイスは稼動状態に戻ります。

-   デバイスは外部イベントを検出し、そのバスで wake シグナルをトリガーします。 カーネルモードバスドライバーは、ウェイクアップ信号を検出します。

-   デバイスはアイドル状態で、ドライバーは[**IWDFDevice2:: StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)を呼び出します。

-   システムの電源状態が低電力状態から動作中 (S0) 状態に変わりました。

このような状況では、カーネルモードバスドライバーによってデバイス (バスの子デバイス) が動作 (D0) 状態に復元されます。

デバイスをサポートする各 UMDF ベースの関数とフィルタードライバーについて、フレームワークは次の処理を一度に1つずつ実行します。ドライバーはドライバースタックの一番下のドライバーから始まります。

1.  フレームワークは、ドライバーの[**IPnpCallback:: OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) callback 関数 (存在する場合) を呼び出します。

2.  ドライバーがデバイスの電源ポリシーの所有者である場合、フレームワークは[**IPowerPolicyCallbackWakeFromS0:: OnDisarmWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)または[**IPowerPolicyCallbackWakeFromSx:: OnDisarmWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx) callback 関数を呼び出します。

3.  フレームワークは、デバイスのすべての電源管理 i/o キューを再起動し、必要に応じて[**IQueueCallbackIoResume:: OnIoResume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackioresume-onioresume) callback 関数を呼び出します。

4.  ドライバーが自己管理型 i/o を使用している場合、フレームワークはドライバーの[**IPnpCallbackSelfManagedIo:: OnSelfManagedIoRestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart) callback 関数を呼び出します。

これらの手順を示す図については、「[デバイスにユーザーが](a-user-plugs-in-a-device.md)接続している」を参照してください。

 

 





