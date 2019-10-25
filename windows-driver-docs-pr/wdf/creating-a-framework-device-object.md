---
title: フレームワーク デバイス オブジェクトの作成
description: フレームワーク デバイス オブジェクトの作成
ms.assetid: 25023c19-a153-4bd4-9fb6-3a1bf85860aa
keywords:
- PnP WDK KMDF、デバイスオブジェクト
- WDK KMDF、デバイスオブジェクトのプラグアンドプレイ
- 電源管理 WDK KMDF、デバイスオブジェクト
- デバイスオブジェクト WDK KMDF
- フレームワークオブジェクト WDK KMDF、デバイスオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f0a1a7e4e819304fe7bbda42537f6ade2ac30be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845619"
---
# <a name="creating-a-framework-device-object"></a>フレームワーク デバイス オブジェクトの作成


すべての関数ドライバー、フィルタードライバー、およびバスドライバーは、システムに接続されているサポート対象デバイスの各インスタンスに対して、フレームワークデバイスオブジェクトを作成する必要があります。

フレームワークデバイスオブジェクトの作成には、次の3つの手順が含まれます。

1.  [**Wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのポインターを取得しています。

    これは、システムによって割り当てられた非透過の構造体で、ドライバーはデバイスに関する情報を格納します。

2.  WDFDEVICE\_INIT 構造体を初期化しています。

    ドライバーは、構造体に情報を追加する、フレームワークが提供する一連の関数を呼び出します。

3.  [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出しています。

    このドライバーは、WDFDEVICE\_INIT 構造体のポインターを**WdfDeviceCreate**メソッドに渡します。 メソッドは、フレームワークデバイスオブジェクトを作成し、WDFDEVICE\_INIT 構造体の情報を使用してオブジェクトを初期化します。

フレームワークデバイスオブジェクトの作成の詳細については、次のトピックを参照してください。

-   [関数ドライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-function-driver.md)

-   [フィルタードライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-filter-driver.md)

-   [バスドライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-bus-driver.md)

 

 





