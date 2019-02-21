---
title: PnP、電源管理インターフェイス
description: PnP、電源管理インターフェイス
ms.assetid: b80228f7-50be-4551-870b-2d7e2b5db239
keywords:
- プラグ アンド プレイ WDK UMDF、電源管理のインターフェイス
- PnP WDK UMDF、電源管理のインターフェイス
- 電源管理 WDK UMDF、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2b71c6c4d38d33d7a0381cc0244b9199731270b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557942"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP、電源管理インターフェイス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

新しいデバイスをシステムに到着すると、フレームワーク、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)到着とパスの UMDF ドライバーに通知するメソッド、 [ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893)と[ **IWDFDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff556965)インターフェイスの呼び出しで。 ドライバーの呼び出し、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899) framework デバイスのデバイス オブジェクトを作成するメソッド。

フレームワーク、ドライバーに通知するために、次のインターフェイスを登録するドライバーは、framework デバイス オブジェクトを作成するときに、インターフェイスに関連付けられているメソッドを呼び出して、— プラグ アンド プレイ (PnP) および電源管理 (PM) のイベントが発生します。

[**IPnpCallback**](https://msdn.microsoft.com/library/windows/hardware/ff556762)

[**IPnpCallbackSelfManagedIo**](https://msdn.microsoft.com/library/windows/hardware/ff556776)

[**IPnpCallbackHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556764)

[**IPowerPolicyCallbackWakeFromS0**](https://msdn.microsoft.com/library/windows/hardware/ff556815)

[**IPowerPolicyCallbackWakeFromSx**](https://msdn.microsoft.com/library/windows/hardware/ff556825)

 

 





