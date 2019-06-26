---
title: GPIO デバイス コンテキスト
description: 汎用の I/O (GPIO) コント ローラー デバイスは、framework デバイス オブジェクトによって表されます。
ms.assetid: 4BE99C71-9BA6-44E3-A54F-DE8C3440A474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d44735cdb30c336c2f57b585b77488494c6865a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363602"
---
# <a name="gpio-device-contexts"></a>GPIO デバイス コンテキスト


汎用の I/O (GPIO) コント ローラー デバイスは、framework デバイス オブジェクトによって表されます。 GPIO コント ローラーのドライバーでは、このデバイス オブジェクトとデバイス コンテキストを関連付けることができます。 ドライバーでは、このデバイス コンテキストを使用して、永続的に GPIO コント ローラーのデバイスの状態に関する情報を格納します。

GPIO フレームワーク拡張機能 (GpioClx) が、ドライバーによって実装されているイベントのコールバック関数を呼び出すと、GpioClx では、この関数に、デバイス コンテキストをパラメーターとして渡します。 コールバック関数は、デバイスの現在の状態を確認するデバイス コンテキストを調べます。 場合は、この関数は、この状態を変更、それに応じて、デバイス コンテキストを更新します。

GpioClx は、デバイス オブジェクトの記憶域を割り当てます。 GPIO コント ローラーのドライバーには、複数のデバイス オブジェクトがある場合は、これらの各オブジェクトのデバイス コンテキスト、同じサイズです。 中に、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン、ドライバーの呼び出し、 [ **GPIO\_CLX\_RegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient)メソッドのコールバック関数を登録して、必要なデバイス コンテキストのサイズを指定します。 後で、中に、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック ルーチン、ドライバーの呼び出し、 [ **GPIO\_CLX\_ProcessAddDevicePostDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate) GpioClx、および GpioClx に新しいデバイス オブジェクトを渡すメソッドがこのオブジェクトに、デバイス コンテキストを割り当てます。 その後、GpioClx がドライバーによって実装されるコールバック関数を呼び出すときにこのデバイス コンテキストに渡されます関数をパラメーターとして。

 

 




