---
title: GPIO デバイス コンテキスト
description: 汎用の I/O (GPIO) コント ローラー デバイスは、framework デバイス オブジェクトによって表されます。
ms.assetid: 4BE99C71-9BA6-44E3-A54F-DE8C3440A474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18038820c85b31fe193472e74df1c9f606444dea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553782"
---
# <a name="gpio-device-contexts"></a>GPIO デバイス コンテキスト


汎用の I/O (GPIO) コント ローラー デバイスは、framework デバイス オブジェクトによって表されます。 GPIO コント ローラーのドライバーでは、このデバイス オブジェクトとデバイス コンテキストを関連付けることができます。 ドライバーでは、このデバイス コンテキストを使用して、永続的に GPIO コント ローラーのデバイスの状態に関する情報を格納します。

GPIO フレームワーク拡張機能 (GpioClx) が、ドライバーによって実装されているイベントのコールバック関数を呼び出すと、GpioClx では、この関数に、デバイス コンテキストをパラメーターとして渡します。 コールバック関数は、デバイスの現在の状態を確認するデバイス コンテキストを調べます。 場合は、この関数は、この状態を変更、それに応じて、デバイス コンテキストを更新します。

GpioClx は、デバイス オブジェクトの記憶域を割り当てます。 GPIO コント ローラーのドライバーには、複数のデバイス オブジェクトがある場合は、これらの各オブジェクトのデバイス コンテキスト、同じサイズです。 中に、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン、ドライバーの呼び出し、 [ **GPIO\_CLX\_RegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/hh439490)メソッドのコールバック関数を登録して、必要なデバイス コンテキストのサイズを指定します。 後で、中に、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック ルーチン、ドライバーの呼び出し、 [ **GPIO\_CLX\_ProcessAddDevicePostDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/hh439484) GpioClx、および GpioClx に新しいデバイス オブジェクトを渡すメソッドがこのオブジェクトに、デバイス コンテキストを割り当てます。 その後、GpioClx がドライバーによって実装されるコールバック関数を呼び出すときにこのデバイス コンテキストに渡されます関数をパラメーターとして。

 

 




