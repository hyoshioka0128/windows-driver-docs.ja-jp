---
title: フレームワーク デバイス オブジェクトの作成
description: フレームワーク デバイス オブジェクトの作成
ms.assetid: 25023c19-a153-4bd4-9fb6-3a1bf85860aa
keywords:
- PnP WDK KMDF、デバイス オブジェクト
- プラグ アンド プレイ WDK KMDF、デバイス オブジェクト
- 電源管理 WDK KMDF、デバイス オブジェクト
- デバイス オブジェクト WDK KMDF
- フレームワークは、WDK KMDF、デバイス オブジェクトをオブジェクトします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0ae33c4247b688b2dba8f851ce1bd6b64a2d68
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383113"
---
# <a name="creating-a-framework-device-object"></a>フレームワーク デバイス オブジェクトの作成


すべての関数のドライバー、フィルター ドライバー、およびバス ドライバーは、システムに接続されているサポートされているデバイスの各インスタンスの framework デバイス オブジェクトを作成する必要があります。

Framework デバイス オブジェクトを作成するには、3 つの手順が含まれます。

1.  ポインターを取得する、 [ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。

    これは、デバイスに関する情報を格納しているドライバーをシステムによって割り当てられた構造体の非透過です。

2.  初期化、WDFDEVICE\_INIT 構造体。

    ドライバーは、一連の構造体に情報を追加するフレームワークが指定した関数を呼び出します。

3.  呼び出す[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

    ドライバーに渡します、WDFDEVICE\_へのポインターを初期化構造体の**WdfDeviceCreate**メソッド。 メソッドは、framework デバイス オブジェクトを作成し、情報を使用して、WDFDEVICE\_INIT 構造オブジェクトを初期化します。

フレームワークにデバイス オブジェクトを作成する方法の詳細については、次のトピックを参照してください。

-   [関数のドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-function-driver.md)

-   [フィルター ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-filter-driver.md)

-   [バス ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-bus-driver.md)

 

 





