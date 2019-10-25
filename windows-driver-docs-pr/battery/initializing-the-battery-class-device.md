---
title: バッテリ クラス デバイスの初期化
description: バッテリ クラス デバイスの初期化
ms.assetid: d385533e-790a-47b3-a3d2-d620cbd40a4d
keywords:
- バッテリクラスドライバー WDK、デバイスの初期化
- バッテリ miniclass ドライバー WDK、登録
- バッテリデバイスの登録
- バッテリデバイスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f62d7119927220f90512f29a0bbefcb38d968f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832220"
---
# <a name="initializing-the-battery-class-device"></a>バッテリ クラス デバイスの初期化


## <span id="ddk_initializing_the_battery_class_device_dg"></span><span id="DDK_INITIALIZING_THE_BATTERY_CLASS_DEVICE_DG"></span>


[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンは、バッテリクラスデバイスを初期化し、miniclass ドライバーをクラスドライバーに登録する必要があります。 これを行うために、miniclass ドライバーは[**BatteryClassInitializeDevice**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice)ルーチンを呼び出します。 この呼び出しは、miniclass ドライバーをクラスドライバーに登録して、2つのドライバーが互いのサポートルーチンを使用できるようにします。 また、この呼び出しによって、バッテリデバイスがシステムに登録され、複合バッテリと電力メーターで認識できるようになります。

**BatteryClassInitializeDevice**には、次の情報を含む[**バッテリ\_ミニポート\_情報**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)構造体へのポインターが必要です。

-   **MajorVersion**と**MinorVersion**で、この miniclass ドライバーがサポートするクラスドライバーのメジャーバージョン番号とマイナーバージョン番号。

    バージョン番号は Batclass として定義されています。これは、\_メジャー\_バージョンとバッテリ\_クラス\_マイナー\_バージョンにそれぞれ\_クラスです。

-   **Querytag**で、miniclass ドライバーの[*BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)ルーチンのエントリポイント。

-   **Queryinformation**で、miniclass ドライバーの[*BatteryMiniQueryInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)ルーチンのエントリポイント。

-   **Setinformation**で、miniclass ドライバーの[*BatteryMiniSetInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_information_callback)ルーチンのエントリポイント。

-   **Setstatusnotify**で、miniclass ドライバーの[*BatteryMiniSetStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)ルーチンのエントリポイント。

-   **Disablestatusnotify**で、miniclass ドライバーの[*BatteryMiniDisableStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)ルーチンのエントリポイント。

-   **コンテキスト**では、miniclass ドライバーのコンテキスト情報へのポインター。

    コンテキスト情報は通常、FDO デバイス拡張機能へのポインターであり、クラスドライバーが[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)ルーチンを呼び出すたびに miniclass ドライバーに渡されます。

-   **Pdo**では、デバイスの pdo へのポインター。

-   **DeviceName**では、NULL パラメーターです。PnP デバイスに名前を指定することはできません。

この構造体を設定した後、miniclass ドライバーは**BatteryClassInitializeDevice**を呼び出し、バッテリ\_ミニポート\_情報構造体へのポインターを渡すことによって、それ自体をバッテリクラスドライバーにアタッチします。 返されると、バッテリクラスドライバーのサポートルーチンへの後続の呼び出しで使用されるハンドルを受け取ります。 Miniclass ドライバーは、返されたクラスハンドルを非ページメモリに格納する必要があります。

**BatteryClassInitializeDevice**を呼び出した後、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンは、デバイス固有のその他のデータを初期化する必要がある場合もあります。

 

 




