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
ms.openlocfilehash: 3dc93f63c6fcab85a2b3a645a266746370eb9ad6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366667"
---
# <a name="obtaining-the-parent-of-a-device-in-the-device-tree"></a>デバイス ツリーでのデバイスの親の取得





このトピックでは、取得する方法を説明します、 **SP_DEVINFO_DATA**) で、デバイス ツリー。

**デバイス ツリー内のデバイスの直接の親の SP_DEVINFO_DATA 構造体を取得するには**

1.  デバイスに devnode があることを確認、[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)呼び出して[ **CM_Get_DevNode_Status** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)デバイス。
    -   デバイスが devnode を持つ場合、関数は CR_SUCCESS を返します。
    -   デバイスが devnode を持たない場合、関数は CR_NO_SUCH_DEVINST を返します。

2.  デバイスに devnode がある場合は、呼び出す[ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)デバイスの親のデバイスのインスタンス ハンドルを取得します。

    (デバイスが、devnode を持たない場合**CM_Get_Parent**ルート デバイスのデバイスのインスタンス ハンドルを返します)。

3.  親デバイスのデバイスのインスタンス ハンドルを使用して、呼び出す[ **CM_Get_Device_ID** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw)親デバイスのデバイス インスタンス ID を取得します。

4.  親デバイスのデバイスのインスタンス ID を使用して、呼び出す[ **SetupDiOpenDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)親デバイス SP_DEVINFO_DATA 構造体を取得します。

**接続されているシーケンス、デバイス、デバイス ツリー内の先祖の SP_DEVINFO_DATA 構造体を取得するには**

-   特定の先祖で終わるおよびデバイスの直接の親から呼び出す**CM_Get_Parent**すべてのハンドルを取得するまで繰り返し。 呼び出しごとに**CM_Get_Parent**装置のデバイスのインスタンス ハンドルは、前の呼び出しから取得します。

-   取得する各デバイス インスタンス ハンドルには、最初に呼び出す**CM_Get_Device_ID**デバイス インスタンス ID を取得し、呼び出す**SetupDiOpenDeviceInfo** SP_DEVINFO_DATA の構造を取得する、デバイスです。

デバイスの存在を操作する方法については、次を参照してください。 [Nonpresent デバイスの親を判断する](determining-the-parent-of-a-nonpresent-device.md)します。

 

 





