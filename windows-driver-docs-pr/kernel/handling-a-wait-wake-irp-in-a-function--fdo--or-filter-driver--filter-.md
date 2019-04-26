---
title: ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理
description: ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理
ms.assetid: 752b6c3c-f42a-469d-8a43-0778ecbe4541
keywords:
- 受信側の待機またはスリープ解除 Irp
- 待機/ウェイク Irp WDK の電源管理の受信
- 関数のドライバー WDK の電源管理
- Fdo WDK の電源管理
- フィルター DOs WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c88994c9d124c8decbe07e6f92729791c6337de9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359818"
---
# <a name="handling-a-waitwake-irp-in-a-function-fdo-or-filter-driver-filter-do"></a>ファンクション ドライバー (FDO) またはフィルター ドライバー (フィルター DO) での待機/ウェイク IRP の処理





FDO またはフィルターを作成するドライバーは受信すると、 [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766) IRP が単に渡すことができますか、関連付けられている PDO を要求して次の下位ドライバーまたは IRP を渡す前に特定のアクションを実行します。

### <a name="for-devices-that-support-wake-up"></a>ウェイク アップをサポートするデバイス

待機/ウェイク IRP を受信すると、関数またはフィルター ドライバーは、以下の手順を実行する必要があります。

1.  呼び出す[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)待機/ウェイク IRP の処理中に要求します。

    場合[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204) 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 IRP が完了する代わりに、([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))、エラー状態を返すとします。

2.  値を検査**Irp -&gt;Parameters.WaitWake.PowerState**で現在のデバイスの電源状態を比較し、 **DeviceState**\[SystemWake\]で、[**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体。

    指定したから、デバイスが、ウェイク アップをサポートしている場合は[SystemWake](systemwake.md)状態または現在のデバイスの電源状態からではなく、ドライバーは IRP を失敗次のようにします。

    -   状態を設定\_無効な\_デバイス\_で状態**Irp -&gt;IoStatus.Status**します。
    -   IRP の完了 (**IoCompleteRequest**)、IO の優先順位を指定する\_いいえ\_インクリメントします。
    -   設定の状態を返す**Irp -&gt;IoStatus.Status**から、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

3.  それ以外の場合、設定、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP を使用して、日常的な[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)します。 *IoCompletion*ルーチンは、ドライバーは、デバイスを動作状態に戻す必要がありますすべてのタスクを実行する必要があります。

    *IoCompletion* IRP が取り消された場合、ルーチンを呼び出すことがもできます。

4.  ドライバーに必要なすべての情報を保存、 *IoCompletion*ルーチン。

5.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (Windows 7、Windows Vista で) または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) (で Windows Server 003、Windows XP、および Windows 2000)次の下位ドライバーには、待機/ウェイク IRP を渡す。

6.  呼び出す[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)以前に取得したロックを解除します。

7.  状態を返す\_から PENDING、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 ドライバーの値を変更する必要があります**Irp -&gt;IoStatus.Status** IRP を保持しています。

### <a name="for-devices-that-do-not-support-wake-up"></a>ウェイク アップをサポートしていないデバイス

関数またはフィルター ドライバー、待機/ウェイク IRP ウェイク アップをサポートしていないデバイスの場合、ドライバーは IRP を次のように、失敗。

1.  IRP の完了 (**IoCompleteRequest**)、IO の優先順位を指定する\_いいえ\_インクリメントします。

2.  設定の状態を返す**Irp -&gt;IoStatus.Status**から、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




