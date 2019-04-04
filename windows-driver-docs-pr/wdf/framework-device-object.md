---
title: Framework デバイス オブジェクト
description: Framework デバイス オブジェクト
ms.assetid: 6be47eac-d6e4-43d1-bf2d-d49dcb2273c0
keywords:
- UMDF オブジェクト WDK、デバイス オブジェクト
- フレームワークは、WDK UMDF、デバイス オブジェクトをオブジェクトします。
- デバイス オブジェクト WDK UMDF
- IWDFDevice
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f8e44cd23797d37b77232f3282970820edb3c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528683"
---
# <a name="framework-device-object"></a>Framework デバイス オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework デバイス オブジェクトが、ドライバーに公開される、 [IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)インターフェイス。 フレームワークのデバイス オブジェクトは、システム上のデバイスのフレームワークの表現です。 各デバイス オブジェクトには、親ドライバー オブジェクトがあります。

新しいデバイスをシステムに到着すると、フレームワーク、 [ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)到着とパスのドライバーに通知するメソッド、 [IWDFDriver](https://msdn.microsoft.com/library/windows/hardware/ff558893)と[IWDFDeviceInitialize](https://msdn.microsoft.com/library/windows/hardware/ff556965)インターフェイスの呼び出しで。 ドライバーは、新しいデバイスを初期化するために IWDFDeviceInitialize インターフェイスのメソッドを呼び出すことができます。 たとえば、ドライバーは、 [ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://msdn.microsoft.com/library/windows/hardware/ff556982)デバイスのインストールの一部として提供されているデバイスについては、クエリ メソッド。 ドライバーを呼び出して、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)メソッドを構成し、デバイス オブジェクトを作成します。

登録するドライバーは、framework デバイス オブジェクトを作成するときに、 [IPnpCallback](https://msdn.microsoft.com/library/windows/hardware/ff556762)、 [IPnpCallbackSelfManagedIo](https://msdn.microsoft.com/library/windows/hardware/ff556776)、 [IPnpCallbackHardware](https://msdn.microsoft.com/library/windows/hardware/ff556764)、 [IFileCallbackCleanup](https://msdn.microsoft.com/library/windows/hardware/ff554902)、および[IFileCallbackClose](https://msdn.microsoft.com/library/windows/hardware/ff554907)インターフェイス。 フレームワークでは、ファイルのクリーンアップと終了し、プラグ アンド プレイ (PnP) と電源管理 (PM) のイベントが発生したときに、ドライバーを通知します。 PnP をサポートしていると PM の詳細については、[UMDF ベースのドライバーでの PnP と電源管理](pnp-and-power-management-in-umdf-drivers.md)を参照してください。

 

 





