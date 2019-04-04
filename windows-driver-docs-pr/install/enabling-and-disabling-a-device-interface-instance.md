---
title: 有効にして、デバイス インターフェイスのインスタンスを無効化
description: 有効にして、デバイス インターフェイスのインスタンスを無効化
ms.assetid: 4e3341c2-ba95-458e-8d92-a35545a773e0
keywords:
- インターフェイス クラス WDK デバイスのインストール
- デバイス インターフェイスのインスタンスを無効にします。
- IoSetDeviceInterfaceState
- デバイスのインターフェイス クラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 060b7777dfdf96937c2c8590cc17c3bad06f3894
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527440"
---
# <a name="enabling-and-disabling-a-device-interface-instance"></a>有効にして、デバイス インターフェイスのインスタンスを無効化





デバイスを正常に起動するには後のインターフェイスに登録されているドライバーを呼び出して[ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)インターフェイス インスタンスを有効にします。 ドライバーによって返されるシンボリック リンクの名前を渡します[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)ブール値と共に**TRUE**インターフェイス インスタンスを有効にします。

ドライバーでは、そのデバイスが正常に開始する場合、に呼び出す必要がありますこのルーチン、プラグ アンド プレイ (PnP) を処理中にマネージャーの[ **IRP_MN_START_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。

IRP_MN_START_DEVICE 要求が完了すると、PnP マネージャーは、それらを要求したカーネル モードまたはユーザー モード コンポーネントをデバイス インターフェイスの到着の通知を発行します。 詳細については、[デバイス インターフェイスの変更通知を登録する](https://msdn.microsoft.com/library/windows/hardware/ff560884)を参照してください。

ドライバーを呼び出し、デバイス インターフェイスのインスタンスを無効にする[ **IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)を渡して、 *SymbolicLinkName*によって返される[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)と**FALSE**の値として*を有効にする*します。

処理する場合、ドライバーがデバイスのインターフェイスを無効にする必要があります、 [ **IRP_MN_SURPRISE_REMOVAL** ](https://msdn.microsoft.com/library/windows/hardware/ff551760)または[ **IRP_MN_REMOVE_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551738)デバイスの要求。 Irp のこれらの削除を処理する場合、ドライバーによるデバイスのインターフェイスは無効する場合、にする必要があります、その後しようとは、デバイスを削除するとき、PnP マネージャーが、インターフェイスを無効になります。

デバイスが停止したときにドライバーが、インターフェイスを無効 ([**IRP_MN_STOP_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551755)); 代わりに、有効な任意のデバイス インターフェイスのままにする必要がありますが、までキューの I/O 要求を受け取る別[ **IRP_MN_START_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 同様に、ドライバー、デバイスがスリープ状態で配置時にそのインターフェイスを無効する必要があります。 デバイスのスリープ状態になるまで、I/O 要求をキューにする必要があります。 詳細については、[サポート デバイスがあるウェイク アップ機能](https://msdn.microsoft.com/library/windows/hardware/ff563907)を参照してください。

 

 





