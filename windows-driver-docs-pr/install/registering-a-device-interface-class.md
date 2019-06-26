---
title: デバイス インターフェイス クラスの登録
description: デバイス インターフェイス クラスの登録
ms.assetid: 1518570d-1cfb-498e-91f7-35f9cc11aff5
keywords:
- インターフェイス クラス WDK デバイスのインストール
- インターフェイス クラスのデバイスの登録
- デバイスのインターフェイス クラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2172cd3d53b20f0442d01e41175bbad248ee8dad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386894"
---
# <a name="registering-a-device-interface-class"></a>デバイス インターフェイス クラスの登録





デバイスのインターフェイス クラスを登録する 3 つの方法はあります。

-   ほとんどのドライバーなどのカーネル モード コンポーネントは、I/O マネージャー ルーチンを呼び出すことができます。 このトピックでは、これらのルーチンを使用する方法について説明します。

-   ユーザー モード*デバイス インストール アプリケーション*呼び出す **SetupDi * * * Xxx*関数。 これらの関数の詳細については、次を参照してください。 [SetupDi デバイス インターフェイス関数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)します。

-   INF ファイルに含めることができます[ **INF DDInstall.Interfaces セクション**](inf-ddinstall-interfaces-section.md)します。

WDM ドライバーでは、そのデバイス オブジェクトを指定しない場合。 代わりに、ドライバーを呼び出すと[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)デバイス オブジェクトを作成するには、デバイス名は null 文字列を指定にする必要があります。 詳細については、次を参照してください。[デバイス オブジェクトを作成する](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-a-device-object)します。

デバイス オブジェクトを作成し、デバイス スタックに接続し後、1 つのドライバーを呼び出して[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)デバイス インターフェイス クラスを登録して、インターフェイスのインスタンスを作成します。 関数のドライバーからのこの呼び出しは、通常、その[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンが、フィルター ドライバーは、インターフェイスを登録します。

ルーチンは、シンボリック リンクの名前を返します。 ドライバーは、有効、または、デバイス インターフェイスのインスタンスを無効にするときに、リンク名を渡します。 他のシステム コンポーネントは、ドライバーが有効になるまで、デバイス インターフェイスのインスタンスを使用できません。 参照してください[を有効にして、デバイス インターフェイスのインスタンスを無効化](enabling-and-disabling-a-device-interface-instance.md)詳細についてはします。

ドライバーでは、デバイス インターフェイスに固有の情報を格納できる、レジストリ キーにアクセスするのにリンクをシンボリック名も使用します。 (を参照してください[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)詳細についてはします)。アプリケーションでは、リンクの名前を使用して、デバイスを開きます。

ドライバーを呼び出すことができます[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)インターフェイスの追加のデバイス クラスのインスタンスを登録するために必要な回数だけです。

 

 





