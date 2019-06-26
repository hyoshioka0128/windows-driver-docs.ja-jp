---
title: デバイス インターフェイス プロパティ値の設定
description: デバイス インターフェイス プロパティ値の設定
ms.assetid: 44cef4e1-9fda-44fb-b37f-342099b5f7a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf0db234ec630d093e175df8f0697ac3b59d91ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378838"
---
# <a name="setting-a-device-interface-property-value"></a>デバイス インターフェイス プロパティ値の設定


値を設定する、[デバイス インターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))Windows Vista および以降のバージョンの Windows では、呼び出す[ **SetupDiSetDeviceInterfaceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)し、次を指定します。パラメーター値:

-   設定*DeviceInfoSet*デバイス インターフェイスのプロパティを設定する対象のデバイスのインターフェイスが含まれるデバイス情報のセットへのハンドル。

-   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)デバイス インターフェイスのプロパティを設定する対象のデバイスのインターフェイスを表す構造体.

-   設定*PropertyKey*へのポインター、 [ **DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)を設定するプロパティを表す構造体です。

-   設定*PropertyType*へのポインターを[ **DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)-型指定された変数を設定するプロパティの識別子のデータ型のプロパティを提供します。

-   設定*PropertyBuffer*プロパティの値を格納しているバッファーへのポインター。

-   設定*PropertyBufferSize*プロパティの値のバイト単位のサイズにします。

-   設定*RequiredSize* DWORD に型指定された変数にします。

-   設定*フラグ*をゼロにします。

場合に呼び出し[ **SetupDiSetDeviceInterfaceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)成功すると、 **SetupDiSetDeviceInterfaceProperty**デバイス クラスのプロパティを設定し、返します**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiSetDeviceInterfaceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





