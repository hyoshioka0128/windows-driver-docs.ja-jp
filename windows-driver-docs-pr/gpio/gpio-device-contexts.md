---
title: GPIO デバイス コンテキスト
description: 汎用 i/o (GPIO) コントローラーデバイスは、フレームワークデバイスオブジェクトによって表されます。
ms.assetid: 4BE99C71-9BA6-44E3-A54F-DE8C3440A474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16cab2778277b72eebc1ecde941a47baa17dba0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824996"
---
# <a name="gpio-device-contexts"></a>GPIO デバイス コンテキスト


汎用 i/o (GPIO) コントローラーデバイスは、フレームワークデバイスオブジェクトによって表されます。 GPIO コントローラードライバーは、デバイスコンテキストをこのデバイスオブジェクトに関連付けることができます。 ドライバーは、このデバイスコンテキストを使用して、GPIO コントローラーデバイスの状態に関する情報を永続的に格納します。

GPIO framework 拡張機能 (GpioClx) が、ドライバーによって実装されているイベントコールバック関数を呼び出すと、GpioClx は、この関数にパラメーターとしてデバイスコンテキストを渡します。 コールバック関数は、デバイスコンテキストを調べて、デバイスの現在の状態を確認します。 関数がこの状態を変更すると、それに応じてデバイスコンテキストが更新されます。

GpioClx は、デバイスオブジェクトのストレージを割り当てます。 GPIO コントローラードライバーに複数のデバイスオブジェクトがある場合、これらの各オブジェクトのデバイスコンテキストは同じサイズになります。 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンでは、ドライバーは[**GPIO\_Clx\_registerclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)メソッドを呼び出して、コールバック関数を登録し、必要なデバイスコンテキストサイズを指定します。 その後、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックルーチンの実行中に、ドライバーは[**GPIO\_Clx\_ProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)メソッドを呼び出して新しいデバイスオブジェクトを gpioclx に渡します。 gpioclx によってデバイスコンテキストが割り当てられます。素材. その後、GpioClx がドライバーによって実装されたコールバック関数を呼び出すと、このデバイスコンテキストはパラメーターとして関数に渡されます。

 

 




