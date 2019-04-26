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
ms.openlocfilehash: b5fd58a579fbdbc46dbfc82f87ef8d88953397c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348180"
---
# <a name="registering-a-device-interface-class"></a>デバイス インターフェイス クラスの登録





デバイスのインターフェイス クラスを登録する 3 つの方法はあります。

-   ほとんどのドライバーなどのカーネル モード コンポーネントは、I/O マネージャー ルーチンを呼び出すことができます。 このトピックでは、これらのルーチンを使用する方法について説明します。

-   ユーザー モード*デバイス インストール アプリケーション*呼び出す **SetupDi * * * Xxx*関数。 これらの関数の詳細については、次を参照してください。 [SetupDi デバイス インターフェイス関数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)します。

-   INF ファイルに含めることができます[ **INF DDInstall.Interfaces セクション**](inf-ddinstall-interfaces-section.md)します。

WDM ドライバーでは、そのデバイス オブジェクトを指定しない場合。 代わりに、ドライバーを呼び出すと[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)デバイス オブジェクトを作成するには、デバイス名は null 文字列を指定にする必要があります。 詳細については、次を参照してください。[デバイス オブジェクトを作成する](https://msdn.microsoft.com/library/windows/hardware/ff542862)します。

デバイス オブジェクトを作成し、デバイス スタックに接続し後、1 つのドライバーを呼び出して[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)デバイス インターフェイス クラスを登録して、インターフェイスのインスタンスを作成します。 関数のドライバーからのこの呼び出しは、通常、その[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンが、フィルター ドライバーは、インターフェイスを登録します。

ルーチンは、シンボリック リンクの名前を返します。 ドライバーは、有効、または、デバイス インターフェイスのインスタンスを無効にするときに、リンク名を渡します。 他のシステム コンポーネントは、ドライバーが有効になるまで、デバイス インターフェイスのインスタンスを使用できません。 参照してください[を有効にして、デバイス インターフェイスのインスタンスを無効化](enabling-and-disabling-a-device-interface-instance.md)詳細についてはします。

ドライバーでは、デバイス インターフェイスに固有の情報を格納できる、レジストリ キーにアクセスするのにリンクをシンボリック名も使用します。 (を参照してください[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)詳細についてはします)。アプリケーションでは、リンクの名前を使用して、デバイスを開きます。

ドライバーを呼び出すことができます[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)インターフェイスの追加のデバイス クラスのインスタンスを登録するために必要な回数だけです。

 

 





