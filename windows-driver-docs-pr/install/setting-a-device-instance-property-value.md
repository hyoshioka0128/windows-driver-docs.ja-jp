---
title: デバイス インスタンス プロパティ値の設定
description: デバイス インスタンス プロパティ値の設定
ms.assetid: 45f63ee3-278e-4b8c-a666-c860074fa172
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a1af94c1bd174891a4829ac770dcc22bf943c2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386889"
---
# <a name="setting-a-device-instance-property-value"></a>デバイス インスタンス プロパティ値の設定


Windows Vista および以降のバージョンの Windows デバイスのインスタンス プロパティの値を設定するには、呼び出す[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)し、次のパラメーター値を指定します。

-   設定*DeviceInfoSet*プロパティを設定する対象のデバイスのインスタンスを含むデバイス情報のセットへのハンドル。

-   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)プロパティを設定する対象のデバイスのインスタンスを表す構造体です。

-   設定*PropertyKey*へのポインター、 [ **DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)を設定するプロパティを表す構造体です。

-   設定*PropertyType*へのポインターを[ **DEVPROPTYPE**](https://docs.microsoft.com/previous-versions/ff543546(v=vs.85))-型指定された変数を設定するプロパティの識別子のデータ型のプロパティを提供します。

-   設定*PropertyBuffer*プロパティの値を格納しているバッファーへのポインター。

-   設定*PropertyBufferSize*プロパティの値のバイト単位のサイズにします。

-   設定*RequiredSize* DWORD に型指定された変数にします。

-   設定*フラグ*をゼロにします。

この呼び出し場合[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)成功すると、 **SetupDiSetDeviceProperty**デバイス インスタンスのプロパティを設定し、返します**TRUE**. 関数呼び出しが失敗した場合、 **SetupDiGetDeviceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





