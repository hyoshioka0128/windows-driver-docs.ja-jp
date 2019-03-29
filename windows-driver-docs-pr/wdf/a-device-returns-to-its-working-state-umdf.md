---
title: デバイスが動作状態に戻る
description: デバイスが動作状態に戻る
ms.assetid: 2b192eea-f731-4d61-be19-95724bf7b04a
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスが稼働状態に戻す
- デバイスの状態のシナリオ WDK UMDF の操作に戻る
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7502f2501251da8668925fc1b070dbb949be5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573538"
---
# <a name="a-device-returns-to-its-working-state"></a>デバイスが動作状態に戻る


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

低電力状態にあるデバイスは、次のいずれかが発生した場合の稼働状態に返されます。

-   デバイスは、外部イベントを検出し、そのバス上ウェイク信号をトリガーします。 カーネル モードのバス ドライバーでは、ウェイク信号を検出します。

-   デバイスがアイドル状態だったし、ドライバーは呼び出し[ **IWDFDevice2::StopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff556948)します。

-   システムの電源の状態は、低電力状態からの作業 (S0) 状態に変更されました。

それぞれの状況では、カーネル モードのバス ドライバーは、作業 (D0) の状態のデバイス (バスの子デバイス) を復元します。

各 UMDF ベース関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799) (存在する) 場合、コールバック関数。

2.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ **IPowerPolicyCallbackWakeFromS0::OnDisarmWakeFromS0** ](https://msdn.microsoft.com/library/windows/hardware/ff556819)または[ **IPowerPolicyCallbackWakeFromSx::OnDisarmWakeFromSx** ](https://msdn.microsoft.com/library/windows/hardware/ff556828)コールバック関数。

3.  フレームワークの再起動のすべてのデバイスの電源管理対象の I/O キューと呼び出しの[ **IQueueCallbackIoResume::OnIoResume** ](https://msdn.microsoft.com/library/windows/hardware/ff556865)コールバック関数 (必要な場合)。

4.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff556785)コールバック関数。

次の手順を示す図を表示するには、次を参照してください。[デバイスで、ユーザーのプラグ](a-user-plugs-in-a-device.md)します。

 

 





