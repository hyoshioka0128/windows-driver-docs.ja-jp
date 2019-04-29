---
title: WDFDEVICE_INIT 構造体
description: WDFDEVICE_INIT 構造体で定義され、フレームワークによって割り当てられた非透過構造です。
ms.assetid: 38a8d316-6d66-4c1a-bb1c-93e2893542e8
keywords:
- WDFDEVICE_INIT 構造体
ms.date: 02/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 26d6a182eb9223512eeaf190ea7ef9f23dfdff5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390838"
---
# <a name="wdfdeviceinit-structure"></a>WDFDEVICE_INIT 構造体


\[KMDF および UMDF に適用されます。\]

**WDFDEVICE_INIT**構造体で定義され、フレームワークによって割り当てられた非透過構造体。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
struct WDFDEVICE_INIT {
  ;      // Reserved.
};
```

<a name="members"></a>メンバー
----------

関数とフィルター ドライバーへの入力としてこの構造体へのポインターを受け取る、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数、またはからの戻り値として[ **WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)します。

バス ドライバーでは、構造体のポインターを受け取るへの入力として、 [ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数、またはからの戻り値として[ **WdfPdoInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate).

ドライバーを受信した後、 **WDFDEVICE_INIT**構造体の初期化関数に構造体のポインターを渡されます。
これらの関数を使用して、 **WDFDEVICE_INIT** framework デバイス オブジェクトを作成するために、フレームワークを使用する情報を格納する構造体。

初期化メソッドをデバイスのドキュメントを見つけるを参照してください。 [wdfdevice.h ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/)します。

初期化関数を呼び出した後、ドライバーを呼び出す必要があります[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate) framework デバイス オブジェクトを作成します。

ドライバーが受信した場合、 **WDFDEVICE_INIT**構造体への呼び出しから[ **WdfPdoInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)または[ **WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)、ドライバーは、初期化関数の呼び出しからエラーを受け取る場合、ドライバーを呼び出す必要がありますと[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)の代わりに[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

ドライバーを呼び出してはならない[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)に成功した呼び出しの後に[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

**WDFDEVICE_INIT**構造体がバージョン 1.0 および KMDF の以降のバージョンで使用できます。


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
<td>Wdftypes.h (Wdftypes.h を含む)</td>
</tr>
</tbody>
</table>


