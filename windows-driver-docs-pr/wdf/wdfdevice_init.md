---
title: WDFDEVICE_INIT 構造体
description: WDFDEVICE_INIT 構造体は、フレームワークによって定義および割り当てられる不透明な構造体です。
ms.assetid: 38a8d316-6d66-4c1a-bb1c-93e2893542e8
keywords:
- WDFDEVICE_INIT 構造体
ms.date: 02/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5398fd39d785a2ff8602f7081bce12c164def7ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845411"
---
# <a name="wdfdevice_init-structure"></a>WDFDEVICE_INIT 構造体


\[KMDF と UMDF\] に適用されます

**WDFDEVICE_INIT**構造体は、フレームワークによって定義および割り当てられる不透明な構造体です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
struct WDFDEVICE_INIT {
  ;      // Reserved.
};
```

<a name="members"></a>Members
----------

関数ドライバーとフィルタードライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数への入力として、または[**Wdfcontroldeviceinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)からの戻り値として、この構造体へのポインターを受け取ります。

バスドライバーは、 [*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数への入力として、または[**Wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)からの戻り値として構造体ポインターを受け取ります。

ドライバーは、 **WDFDEVICE_INIT**構造体を受け取ると、構造体ポインターを初期化関数に渡します。
これらの関数は、フレームワークがフレームワークデバイスオブジェクトを作成するために使用する情報を格納するために、 **WDFDEVICE_INIT**構造体を使用します。

デバイスの初期化方法に関するドキュメントについては、「 [wdfdevice. h ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)」を参照してください。

初期化関数を呼び出した後、ドライバーは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、フレームワークデバイスオブジェクトを作成する必要があります。

ドライバーが[**Wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)または[**Wdfcontroldeviceinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)の呼び出しから**WDFDEVICE_INIT**構造体を受信し、ドライバーが初期化関数の呼び出しからエラーを受信した場合、ドライバーは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)ではなく[**wdfpdoinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)を呼び出す必要があります。

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)への呼び出しが成功した後、ドライバーは[**Wdfdeviceinitfree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)を呼び出さないでください。

**WDFDEVICE_INIT**構造は、バージョン1.0 以降の kmdf で使用できます。


<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdftypes .h (Wdftypes. h を含む)</td>
</tr>
</tbody>
</table>


