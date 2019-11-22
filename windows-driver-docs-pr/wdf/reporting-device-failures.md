---
title: デバイスの障害の報告
description: デバイスの障害の報告
ms.assetid: ca536547-d51a-4450-8a83-19aac67aab92
keywords:
- PnP WDK KMDF、デバイスエラー
- WDK KMDF のプラグアンドプレイ、デバイスの障害
- デバイス障害 (WDK KMDF)
- 失敗したデバイスの WDK KMDF
- WdfDeviceFailedAttemptRestart
- WdfDeviceFailedNoRestart
- デバイスエラーの報告 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90dc924ad4c7cb0d36e3098d0c5b8084e6024021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842210"
---
# <a name="reporting-device-failures"></a>デバイスの障害の報告


デバイスの障害を報告するには、次の3つの方法があります。

-  [デバイスオブジェクトコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-callbacks)から制御が戻るときに、ドライバーは、 [NT\_SUCCESS](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)(*状態*) が**FALSE**になる戻り値を指定できます。

-  ドライバーは[**Wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)を呼び出すことができます。

-  [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックルーチンから制御が戻るときに、関数ドライバーは、 [NT\_SUCCESS](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)(*状態*) が**FALSE**になる戻り値を指定できます。 [フィルタ]( https://docs.microsoft.com/en-us/windows-hardware/drivers/install/installing-a-filter-driver)としてインストールされたドライバが[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)に失敗した場合、オペレーティングシステムはフィルタデバイスオブジェクトをスキップし、PnP エラーを示しません。

上記の方法では、フレームワークによってデバイスが実質的に削除されます。 デバイスのドライバーがシステム上の他のデバイスをサポートしていない場合は、i/o マネージャーによってドライバーがアンロードされます。

ドライバーのデバイスオブジェクトコールバック関数が、NT\_SUCCESS (*状態*) が**FALSE**に等しい値を返した場合、フレームワークは PnP マネージャーに通知します。これにより、バスドライバーによってデバイスの再起動が試行されます。ハードウェア. ドライバーがアンロードされた場合は、再読み込みされます。

ドライバーが[**Wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)を呼び出すと、デバイスを再起動するかどうかを決定する入力引数が提供されます。 引数の値は**Wdfdevicefailedattemptrestart**と**WdfDeviceFailedNoRestart**です。

**UMDF**UMDF 2.15 より前の場合、UMDF ドライバーはこの値を**WdfDeviceFailedNoRestart**に設定する必要があります。 UMDF バージョン2.15 以降では、UMDF ドライバーは、失敗した*アクション*を**Wdfdevicefailedattemptrestart**に設定して、 [**wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)呼び出して、基になるバスドライバーが再列挙するように要求できます。 詳細については、「 [**Wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)」を参照してください。 

これらの引数値の詳細については、「 [**WDF\_DEVICE\_FAILED\_ACTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_device_failed_action)」を参照してください。
ドライバーのデバイスオブジェクトコールバック関数が、NT\_SUCCESS (*状態*) が**FALSE**に設定された値で返される前に、コールバック関数は、 **WdfDeviceFailedNoRestart**の入力引数で[**wdfdevicesetfailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)を呼び出すことによって再起動を防ぐことができます。 それ以外の場合、これらのコールバック関数は**Wdfdevicesetfailed**を呼び出す必要はありません。

短時間以内に複数回の再起動が失敗した場合 (再起動されたドライバーによってエラーが再度報告される)、フレームワークはデバイスの再起動を停止します。

バスドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)関数が、NT\_SUCCESS (*状態*) が**FALSE**に等しい値を返した場合、このフレームワークは、バスドライバーに関連付けられているドライバーの*EvtDeviceD0Entry*関数を呼び出す可能性があります。子デバイス。

 

 





