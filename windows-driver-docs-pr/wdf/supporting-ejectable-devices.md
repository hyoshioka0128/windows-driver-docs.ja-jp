---
title: 取り出し可能デバイスのサポート
description: 取り出し可能デバイスのサポート
ms.assetid: 7820bb71-7218-4c5f-af2b-f41e1b5f696d
keywords:
- PnP WDK KMDF、ejectable デバイス
- プラグアンドプレイ WDK KMDF、ejectable デバイス
- 電源管理 WDK KMDF、ejectable デバイス
- ドッキングステーション WDK KMDF
- バスドライバー WDK KMDF
- デバイスの取り出し (WDK KMDF)
- 排出関係 WDK KMDF
- ejectable デバイスの削除
- ejectable devices WDK KMDF の一覧表示
- ejectable デバイスをロックする WDK KMDF
- ポータブルデバイス WDK KMDF
- モバイルデバイス WDK、KMDF
- リムーバブルデバイスの WDK KMDF
- モバイルデバイス WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7906c466a2f0511bf99a469cdef9b2718827ae31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831994"
---
# <a name="supporting-ejectable-devices"></a>取り出し可能デバイスのサポート


*Ejectable デバイス*は、ドッキングステーションに挿入し、ドッキングステーションから取り出すことができるデバイスです。 通常、デバイスを削除する前に、ejectable デバイスのバス電源を無効にする必要があります。

デバイスが ejectable の場合、デバイスのバスのバスドライバーは、デバイスの[**WDF\_デバイス\_PNP\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)の構造体の**EjectSupported**メンバーを設定する必要があります。

バスドライバーは、列挙された子デバイスの1つが取り出しようとしていると判断したときに、 [**WdfPdoRequestEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdorequesteject)または[**WdfChildListRequestChildEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)を呼び出します。 たとえば、バスドライバーは、ユーザーが取り出しボタンを押したことを検出する場合があります。

ドライバーが[**WdfChildListRequestChildEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)または[**WdfPdoRequestEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdorequesteject)を呼び出すと、PnP マネージャーは、デバイスが削除されていることをデバイスのドライバーに通知するために、[正常な削除](a-user-unplugs-a-device.md#orderly-removal)のシナリオを使用します。 フレームワークは、デバイスのバスのバスドライバーで[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware) callback 関数を呼び出した後、バスドライバーの[*Evtdeviceeject*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)コールバック関数を呼び出します。これにより、デバイスを物理的に取り出します。

デバイスの取り出しによって追加のデバイスも排出されると、バスドライバーは*取り出し関係*のリストを保持できます。 ユーザーがデバイスを削除すると、デバイスが削除されていることをリスト内のデバイスのドライバーに通知します。 [**WdfPdoAddEjectionRelationsPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoaddejectionrelationsphysicaldevice)、 [**WdfPdoRemoveEjectionRelationsPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoremoveejectionrelationsphysicaldevice)、および[**WdfPdoClearEjectionRelationsDevices**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoclearejectionrelationsdevices)の各メソッドを使用すると、排出関係のリストを保持できます。

ドッキングステーションでデバイスをロックできる場合、バスドライバーはデバイスの WDF\_デバイスの**locksupported**メンバー [ **\_PNP\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)構造体を設定する必要があります。 バスドライバーは、 [*Evtdevicesetlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)コールバック関数も提供する必要があります。これにより、デバイスをロックして、排出を無効にしたり、デバイスのロックを解除したりすることができます。

 

 





