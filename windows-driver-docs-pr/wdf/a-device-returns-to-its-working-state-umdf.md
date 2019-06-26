---
title: デバイスが動作状態に戻る
description: デバイスが動作状態に戻る
ms.assetid: 2b192eea-f731-4d61-be19-95724bf7b04a
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスが稼働状態に戻す
- デバイスの状態のシナリオ WDK UMDF の操作に戻る
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4632df1c4725dc0888ea611187bc2bd5ca0723a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385335"
---
# <a name="a-device-returns-to-its-working-state"></a>デバイスが動作状態に戻る


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

低電力状態にあるデバイスは、次のいずれかが発生した場合の稼働状態に返されます。

-   デバイスは、外部イベントを検出し、そのバス上ウェイク信号をトリガーします。 カーネル モードのバス ドライバーでは、ウェイク信号を検出します。

-   デバイスがアイドル状態だったし、ドライバーは呼び出し[ **IWDFDevice2::StopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-stopidle)します。

-   システムの電源の状態は、低電力状態からの作業 (S0) 状態に変更されました。

それぞれの状況では、カーネル モードのバス ドライバーは、作業 (D0) の状態のデバイス (バスの子デバイス) を復元します。

各 UMDF ベース関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ **IPnpCallback::OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) (存在する) 場合、コールバック関数。

2.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ **IPowerPolicyCallbackWakeFromS0::OnDisarmWakeFromS0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefroms0-ondisarmwakefroms0)または[ **IPowerPolicyCallbackWakeFromSx::OnDisarmWakeFromSx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipowerpolicycallbackwakefromsx-ondisarmwakefromsx)コールバック関数。

3.  フレームワークの再起動のすべてのデバイスの電源管理対象の I/O キューと呼び出しの[ **IQueueCallbackIoResume::OnIoResume** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackioresume-onioresume)コールバック関数 (必要な場合)。

4.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediorestart)コールバック関数。

次の手順を示す図を表示するには、次を参照してください。[デバイスで、ユーザーのプラグ](a-user-plugs-in-a-device.md)します。

 

 





