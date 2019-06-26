---
title: デバイスの障害の報告
description: デバイスの障害の報告
ms.assetid: ca536547-d51a-4450-8a83-19aac67aab92
keywords:
- PnP WDK KMDF、デバイスの障害
- プラグ アンド プレイ WDK KMDF、デバイスの障害
- デバイスの障害 WDK KMDF
- 失敗したデバイス WDK KMDF
- WdfDeviceFailedAttemptRestart
- WdfDeviceFailedNoRestart
- デバイスの失敗 WDK KMDF の報告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 265288ede02f6bea67d4b8851ec1ae6dbc81eb1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376286"
---
# <a name="reporting-device-failures"></a>デバイスの障害の報告


デバイスの失敗を報告する 2 つの方法はあります。

-   戻るときに[デバイス オブジェクトのコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#device-callbacks)、ドライバーは、対象の戻り値を指定できます[NT\_成功](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)(*状態*)に等しい**FALSE**します。

-   ドライバーが呼び出せる[ **WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)します。

どちらの方法では、フレームワークは実質的に、デバイスを削除します。 デバイスのドライバーでは、システム上の他のデバイスはサポートされていません、I/O マネージャーは、ドライバーをアンロードします。

ドライバーのデバイス オブジェクトのコールバック関数がどの NT の値を返す場合\_成功 (*状態*) と等しい**FALSE**フレームワークに通知を再起動しようとし、PnP マネージャー、バスの運転手がそのデバイスを再列挙を要求することでデバイスです。 読み込まれていた場合、ドライバーを再読み込みされます。

ドライバーを呼び出す場合[ **WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)デバイスを再起動するかどうかを決定する、入力引数が指定されています。 引数の値が**WdfDeviceFailedAttemptRestart**と**WdfDeviceFailedNoRestart**します。

**UMDF** A UMDF ドライバーはこの値を設定する必要があります**WdfDeviceFailedNoRestart**します。

これらの引数値の詳細については、次を参照してください。 [ **WDF\_デバイス\_FAILED\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ne-wdfdevice-_wdf_device_failed_action)します。
ドライバーのデバイスの前にオブジェクト コールバック関数が返す値を持つどの nt\_成功 (*状態*) と等しい**FALSE**、コールバック関数がを呼び出して再起動を防ぐことができます[ **WdfDeviceSetFailed** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)の入力引数を持つ**WdfDeviceFailedNoRestart**します。 それ以外の場合、これらのコールバック関数を呼び出す必要はありません**WdfDeviceSetFailed**します。

短時間で数回連続して再起動の試行が失敗するは、(再起動、ドライバーは、もう一度、エラーを報告) ため、フレームワークは、デバイスを再起動しようとしています。 停止します。

場合は、バス ドライバーの[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)関数は、どの NT の値を返します\_成功 (*状態*) と等しい**FALSE**、フレームワークが呼び出すことができますが、 *EvtDeviceD0Entry*関数ドライバー、バス ドライバーの子のデバイスに関連付けられているのです。

 

 





