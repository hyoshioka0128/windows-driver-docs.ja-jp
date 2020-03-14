---
title: デバイス停止要求の処理
description: デバイス停止要求の処理
ms.assetid: 4c8f37b3-7961-4c78-a88b-3eec58155e66
keywords:
- PnP WDK KMDF、デバイスの停止
- WDK KMDF のプラグアンドプレイ、デバイスの停止
- リソースの再配布 (WDK KMDF)
- リソース再配布 (WDK KMDF)
- WDK KMDF デバイスの削除
- デバイス停止要求 WDK KMDF
- デバイス停止要求 WKD KMDF、PnP
- 一時的なデバイスの停止 WDK KMDF
- 一時的なデバイスの停止 WDK KMDF、PnP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 095f190f07ef38e22b496081ca73ba136487e01a
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242911"
---
# <a name="handling-requests-to-stop-a-device"></a>デバイス停止要求の処理


デバイスのドライバーに対してデバイスの停止を要求する前に、次の2つの状況が考えられます。デバイスを停止している場合は、PnP マネージャーによってドライバーが要求されます。

-   ユーザーが新しいデバイスに接続し、新しいデバイスに対応するために、PnP マネージャーが[システムのハードウェアリソース](#redistributing-resources)を再配布する必要があります。

-   ユーザーは[、デバイスを削除](#a-user-removes-or-disables-a-device)するように指定しています。

ドライバーでは、次のような状況に対処する方法がいくつかあります。

-   デバイスが特別なファイルをサポートしていて、デバイスで特別なファイルが開いている場合、デバイスの停止をフレームワークで許可しないため、ドライバーが[**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)を呼び出しています。

-   一時的にすべての業務中断を比較的短い時間だけ回避するために、ドライバーは[**Wdfdevicesetstaticstopremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetstaticstopremove)を呼び出すことができます。

-   各停止試行を個別に評価して処理するために、ドライバーは[*Evtdevicequerystop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)および[*Evtdevicequerystop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)コールバック関数を提供できます。

デバイスが特別なファイルをサポートしていない場合、デバイスの停止または削除がドライバーまたはデバイスで問題にならない場合、ドライバーは*Evtdevicequerystop*および*evtdevicequerystop*コールバック関数を提供せず、 **Wdfdevicesetstaticstopremove**を呼び出しません。 この場合、PnP マネージャーは、ドライバーで許可されているかどうかを最初に確認せずに、常にデバイスを停止します。

### <a href="" id="redistributing-resources"></a>リソースの再配布

場合によっては、PnP マネージャーがシステムのハードウェアリソースを再配布する必要があります。 通常、この再配布は、新しいデバイスが接続されていることをバスドライバーが報告し、新しいデバイスに既に割り当てられているリソースが必要であるために発生します。 リソースを再割り当てする前に、デバイスを停止する必要があります。

ドライバーが PnP マネージャーによるビジー状態のデバイスの停止を防ぐ必要がある場合、ドライバーは[*Evtdevicequerystop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)コールバック関数を提供できます。 ドライバーの*Evtdevicequerystop*コールバック関数からエラー状態値が返された場合、PnP マネージャーはデバイスを停止しません。

ドライバーによってデバイスの停止が安全であると判断された場合は、コールバック関数によって STATUS\_SUCCESS が返されます。 デバイスの他のどのドライバーも停止できない場合は、PnP マネージャーによって一時的にデバイスが停止されます。

PnP マネージャーがデバイスを停止してリソースを再配布するときに、フレームワークがドライバーのイベントコールバック関数を呼び出す順序の詳細については、「 [Pnp マネージャーによるシステムリソース](the-pnp-manager-redistributes-system-resources.md)の再配布」を参照してください。

### <a href="" id="a-user-removes-or-disables-a-device"></a>ユーザーがデバイスを削除または無効にする

ユーザーは、一部のデバイスを削除または無効にすることができます。 例 :

-   ドライバーがデバイスの[**WDF\_デバイス\_PNP\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_pnp_capabilities)の構造の**リムーバブル**メンバー ( **SurpriseRemovalOK**メンバーではない) を設定している場合、ユーザーは、デバイスを取り外したり取り出したりすることができます。

-   ドライバーがデバイスの[**WDF\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_state)構造の**notdisableable**メンバーを設定していない場合、ユーザーはデバイスマネージャーを使用してデバイスを無効にすることができます。

このような場合は、ユーザーがデバイスを削除する前に、PnP マネージャーによってデバイスの停止が試行されます。

ドライバーがビジー状態のデバイスを削除できないようにする必要がある場合、ドライバーは[*Evtdevicequeryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)コールバック関数を提供できます。 ドライバーの*Evtdevicequeryremove*コールバック関数からエラー状態値が返された場合、PnP マネージャーはデバイスを停止しません。

ユーザーがデバイスを削除するのが安全であるとドライバーが判断した場合、コールバック関数は状態\_SUCCESS を返します。 デバイスのその他のドライバーが削除できない場合は、PnP マネージャーによってデバイスが停止されます。

デバイスの削除を停止するときに、フレームワークがドライバーのイベントコールバック関数を呼び出す順序の詳細については、「[ユーザーによるデバイスの Unplugs](a-user-unplugs-a-device.md)」を参照してください。

 

 





