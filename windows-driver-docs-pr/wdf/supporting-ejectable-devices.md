---
title: 取り出し可能デバイスのサポート
description: 取り出し可能デバイスのサポート
ms.assetid: 7820bb71-7218-4c5f-af2b-f41e1b5f696d
keywords:
- PnP WDK KMDF、フロッピー デバイス
- プラグ アンド プレイ WDK KMDF、フロッピー デバイス
- 電源管理 WDK KMDF、フロッピー デバイス
- WDK KMDF のドッキング ステーション
- バス ドライバー WDK KMDF
- デバイス WDK KMDF の取り出し
- 取り出し関係 WDK KMDF
- 移動可能なリムーバブル デバイスの削除
- 移動可能なリムーバブル デバイス WDK KMDF を一覧表示します。
- WDK KMDF の移動可能なリムーバブル デバイスのロック
- WDK KMDF のポータブル デバイス
- モバイル デバイス、WDK KMDF
- リムーバブル デバイス WDK KMDF
- WDK のモバイル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f6d1bf883ef0306caab428139eb582bf2148c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368661"
---
# <a name="supporting-ejectable-devices"></a>取り出し可能デバイスのサポート


*移動可能なリムーバブル デバイス*デバイスがドッキング ステーションに挿入され、ドッキング ステーションから取り出すことができます。 通常、デバイスを削除する前に移動可能なリムーバブル デバイスのバスの電源は無効にする必要があります。

デバイスができる場合は、デバイスのバスのバス ドライバーを設定する必要があります、 **EjectSupported**メンバーで、デバイスの[ **WDF\_デバイス\_PNP\_機能** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)構造体。

いずれかを呼び出す、バス ドライバーは、約を取り出すにその列挙子のデバイスのいずれかが判断した場合[ **WdfPdoRequestEject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdorequesteject)または[ **WdfChildListRequestChildEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)します。 たとえば、バス ドライバーは、ユーザーに取り出しボタンが押されたことを検出することがあります。

ドライバーを呼び出すと[ **WdfChildListRequestChildEject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nf-wdfchildlist-wdfchildlistrequestchildeject)または[ **WdfPdoRequestEject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdorequesteject)、PnP マネージャーを使用して、 [正しく削除](a-user-unplugs-a-device.md#orderly-removal)シナリオに、デバイスが削除されることをデバイスのドライバーに通知します。 フレームワークが呼び出された後、 [ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)フレームワークであるデバイスのバスのバス ドライバーでのコールバック関数呼び出す、バス ドライバーの[ *EvtDeviceEject* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)を物理的にデバイスを取り出すために必要なすべての操作を実行するコールバック関数。

バス ドライバーのリストを維持できる追加のデバイスを取り出すにも発生すると、デバイスを取り出し、*取り出し関係*します。 ユーザーは、デバイスを削除するとき、PnP マネージャーは自分のデバイスも削除すること、リスト内のデバイスのドライバーを通知します。 取り出し関係の一覧を維持するために、バス ドライバーを使用して、 [ **WdfPdoAddEjectionRelationsPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoaddejectionrelationsphysicaldevice)、 [ **WdfPdoRemoveEjectionRelationsPhysicalDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoremoveejectionrelationsphysicaldevice)、および[ **WdfPdoClearEjectionRelationsDevices** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoclearejectionrelationsdevices)メソッド。

バス ドライバーを設定する必要があります、ドッキング ステーションにデバイスをロックできる場合、 **LockSupported**メンバーで、デバイスの[ **WDF\_デバイス\_PNP\_機能** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)構造体。 バス ドライバーを提供する必要がありますも、 [ *EvtDeviceSetLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)の取り出しを無効にするデバイスをロックまたは取り出しを有効にするデバイスのロックを解除するコールバック関数。

 

 





