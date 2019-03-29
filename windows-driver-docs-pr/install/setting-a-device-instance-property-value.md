---
title: デバイス インスタンス プロパティ値の設定
description: デバイス インスタンス プロパティ値の設定
ms.assetid: 45f63ee3-278e-4b8c-a666-c860074fa172
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eddc4aa09a80623892db2651363fdb8e097dd471
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580537"
---
# <a name="setting-a-device-instance-property-value"></a>デバイス インスタンス プロパティ値の設定


Windows Vista および以降のバージョンの Windows デバイスのインスタンス プロパティの値を設定するには、呼び出す[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)し、次のパラメーター値を指定します。

-   設定*DeviceInfoSet*プロパティを設定する対象のデバイスのインスタンスを含むデバイス情報のセットへのハンドル。

-   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)プロパティを設定する対象のデバイスのインスタンスを表す構造体です。

-   設定*PropertyKey*へのポインター、 [ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)を設定するプロパティを表す構造体です。

-   設定*PropertyType*へのポインターを[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-型指定された変数を設定するプロパティの識別子のデータ型のプロパティを提供します。

-   設定*PropertyBuffer*プロパティの値を格納しているバッファーへのポインター。

-   設定*PropertyBufferSize*プロパティの値のバイト単位のサイズにします。

-   設定*RequiredSize* DWORD に型指定された変数にします。

-   設定*フラグ*をゼロにします。

この呼び出し場合[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)成功すると、 **SetupDiSetDeviceProperty**デバイス インスタンスのプロパティを設定し、返します**TRUE**. 関数呼び出しが失敗した場合、 **SetupDiGetDeviceProperty**返します**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

 

 





