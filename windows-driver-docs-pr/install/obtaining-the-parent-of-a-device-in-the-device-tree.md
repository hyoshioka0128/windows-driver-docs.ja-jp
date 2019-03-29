---
title: デバイス ツリーでのデバイスの親の取得
description: デバイス ツリーでのデバイスの親の取得
ms.assetid: 0ac1ccbb-c926-4d14-975e-127159309361
keywords:
- SetupAPI 関数 WDK、保護者の方を決定します。
- WDK SetupAPI を決定する親デバイス
- デバイスの親 WDK
- SP_DEVINFO_DATA
- WDK の先祖の接続されているシーケンス
- WDK の先祖
- デバイスの直接の親ツリー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1adc2c37dbbcfc164eeef73fa99853abde93a1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577827"
---
# <a name="obtaining-the-parent-of-a-device-in-the-device-tree"></a>デバイス ツリーでのデバイスの親の取得





このトピックでは、取得する方法を説明します、 **SP_DEVINFO_DATA**) で、デバイス ツリー。

**デバイス ツリー内のデバイスの直接の親の SP_DEVINFO_DATA 構造体を取得するには**

1.  デバイスに devnode があることを確認、[デバイス ツリー](https://msdn.microsoft.com/library/windows/hardware/ff543194)呼び出して[ **CM_Get_DevNode_Status** ](https://msdn.microsoft.com/library/windows/hardware/ff538514)デバイス。
    -   デバイスが devnode を持つ場合、関数は CR_SUCCESS を返します。
    -   デバイスが devnode を持たない場合、関数は CR_NO_SUCH_DEVINST を返します。

2.  デバイスに devnode がある場合は、呼び出す[ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)デバイスの親のデバイスのインスタンス ハンドルを取得します。

    (デバイスが、devnode を持たない場合**CM_Get_Parent**ルート デバイスのデバイスのインスタンス ハンドルを返します)。

3.  親デバイスのデバイスのインスタンス ハンドルを使用して、呼び出す[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)親デバイスのデバイス インスタンス ID を取得します。

4.  親デバイスのデバイスのインスタンス ID を使用して、呼び出す[ **SetupDiOpenDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff552071)親デバイス SP_DEVINFO_DATA 構造体を取得します。

**接続されているシーケンス、デバイス、デバイス ツリー内の先祖の SP_DEVINFO_DATA 構造体を取得するには**

-   特定の先祖で終わるおよびデバイスの直接の親から呼び出す**CM_Get_Parent**すべてのハンドルを取得するまで繰り返し。 呼び出しごとに**CM_Get_Parent**装置のデバイスのインスタンス ハンドルは、前の呼び出しから取得します。

-   取得する各デバイス インスタンス ハンドルには、最初に呼び出す**CM_Get_Device_ID**デバイス インスタンス ID を取得し、呼び出す**SetupDiOpenDeviceInfo** SP_DEVINFO_DATA の構造を取得する、デバイスです。

デバイスの存在を操作する方法については、次を参照してください。 [Nonpresent デバイスの親を判断する](determining-the-parent-of-a-nonpresent-device.md)します。

 

 





