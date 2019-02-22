---
title: デバイスが省電力状態に入る
description: デバイスが省電力状態に入る
ms.assetid: c3697272-75ec-4de5-b123-3d1c68d2044e
keywords:
- 電源管理のシナリオ WDK UMDF、低電力状態に移行します。
- 低電力状態シナリオ WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e59be072171bff0ac111d6ca0c69d7a1bf776208
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553436"
---
# <a name="a-device-enters-a-low-power-state"></a>デバイスが省電力状態に入る


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスは、その動作 (D0) 状態のままし、次のいずれかが発生した場合は低電力状態になります。

-   デバイスがアイドル状態 (にアクセスしていない) のシステムでの作業 (S0) 状態のまま、低電力アイドル状態を入力することができます。

-   システムの電源の状態は、低電力状態にその動作 (S0) 状態から変更されました。 (ドライバーを呼び出すことができます[ **IWDFDevice2::GetSystemPowerAction** ](https://msdn.microsoft.com/library/windows/hardware/ff556936)システムの電源状態の変更の理由を特定します)。

各 UMDF ベース関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最上位である driver 以降では、シーケンスで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoSuspend** ](https://msdn.microsoft.com/library/windows/hardware/ff556790)コールバック関数。

2.  フレームワークを停止すると、すべてのデバイスの電源管理対象の I/O キューと呼び出しの[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoStop** ](https://msdn.microsoft.com/library/windows/hardware/ff556787)コールバック関数 (存在する場合)。

3.  ドライバーがデバイスの電源ポリシーの所有者である場合は、フレームワーク、 [ **IPowerPolicyCallbackWakeFromS0::OnArmWakeFromS0** ](https://msdn.microsoft.com/library/windows/hardware/ff556817)または[ **IPowerPolicyCallbackWakeFromSx::OnArmWakeFromSx** ](https://msdn.microsoft.com/library/windows/hardware/ff556826)コールバック関数。

4.  フレームワークは、ドライバーの[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803) (存在する) 場合、コールバック関数。

次の手順を示す図を表示するには、図計画的な削除を参照してください。[ユーザーがデバイスから切り離し](a-user-unplugs-a-device.md)します。

 

 





