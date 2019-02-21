---
title: Framework デバイス オブジェクトを作成します。
description: Framework デバイス オブジェクトを作成します。
ms.assetid: 25023c19-a153-4bd4-9fb6-3a1bf85860aa
keywords:
- PnP WDK KMDF、デバイス オブジェクト
- プラグ アンド プレイ WDK KMDF、デバイス オブジェクト
- 電源管理 WDK KMDF、デバイス オブジェクト
- デバイス オブジェクト WDK KMDF
- フレームワークは、WDK KMDF、デバイス オブジェクトをオブジェクトします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f94a1a8a2989fb80d3f497eb0613974ab32928ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558278"
---
# <a name="creating-a-framework-device-object"></a>Framework デバイス オブジェクトを作成します。


すべての関数のドライバー、フィルター ドライバー、およびバス ドライバーは、システムに接続されているサポートされているデバイスの各インスタンスの framework デバイス オブジェクトを作成する必要があります。

Framework デバイス オブジェクトを作成するには、3 つの手順が含まれます。

1.  ポインターを取得する、 [ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。

    これは、デバイスに関する情報を格納しているドライバーをシステムによって割り当てられた構造体の非透過です。

2.  初期化、WDFDEVICE\_INIT 構造体。

    ドライバーは、一連の構造体に情報を追加するフレームワークが指定した関数を呼び出します。

3.  呼び出す[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。

    ドライバーに渡します、WDFDEVICE\_へのポインターを初期化構造体の**WdfDeviceCreate**メソッド。 メソッドは、framework デバイス オブジェクトを作成し、情報を使用して、WDFDEVICE\_INIT 構造オブジェクトを初期化します。

フレームワークにデバイス オブジェクトを作成する方法の詳細については、次のトピックを参照してください。

-   [関数のドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-function-driver.md)

-   [フィルター ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-filter-driver.md)

-   [バス ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-bus-driver.md)

 

 





