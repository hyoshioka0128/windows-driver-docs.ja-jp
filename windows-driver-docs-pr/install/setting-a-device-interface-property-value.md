---
title: デバイス インターフェイス プロパティ値の設定
description: デバイス インターフェイス プロパティ値の設定
ms.assetid: 44cef4e1-9fda-44fb-b37f-342099b5f7a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 161d04af5bfe72d8129bdc4b97467570d878fe91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582147"
---
# <a name="setting-a-device-interface-property-value"></a>デバイス インターフェイス プロパティ値の設定


値を設定する、[デバイス インターフェイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409)Windows Vista および以降のバージョンの Windows では、呼び出す[ **SetupDiSetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552158)し、次を指定します。パラメーター値:

-   設定*DeviceInfoSet*デバイス インターフェイスのプロパティを設定する対象のデバイスのインターフェイスが含まれるデバイス情報のセットへのハンドル。

-   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)デバイス インターフェイスのプロパティを設定する対象のデバイスのインターフェイスを表す構造体.

-   設定*PropertyKey*へのポインター、 [ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)を設定するプロパティを表す構造体です。

-   設定*PropertyType*へのポインターを[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-型指定された変数を設定するプロパティの識別子のデータ型のプロパティを提供します。

-   設定*PropertyBuffer*プロパティの値を格納しているバッファーへのポインター。

-   設定*PropertyBufferSize*プロパティの値のバイト単位のサイズにします。

-   設定*RequiredSize* DWORD に型指定された変数にします。

-   設定*フラグ*をゼロにします。

場合に呼び出し[ **SetupDiSetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552158)成功すると、 **SetupDiSetDeviceInterfaceProperty**デバイス クラスのプロパティを設定し、返します**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiSetDeviceInterfaceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





