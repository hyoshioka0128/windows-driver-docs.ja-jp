---
title: USB インターフェイスの使用
description: USB インターフェイスの使用
ms.assetid: 6a1801e4-bd46-4a78-8c30-7dc62e41a37a
keywords:
- USB I/O ターゲット WDK KMDF、USB インターフェイス
- USB インターフェイス WDK KMDF
- framework オブジェクト WDK KMDF、USB インターフェイス オブジェクト
- インターフェイス オブジェクト WDK KMDF
- 代替の WDK KMDF USB インターフェイス設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 738e982145d760505882610f00f605f45db24f4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383535"
---
# <a name="working-with-usb-interfaces"></a>USB インターフェイスの使用


フレームワークとして各 USB インターフェイスを表す、 *framework USB インターフェイス オブジェクト*します。 ときに、ドライバー [framework USB デバイス オブジェクトを作成する](working-with-usb-devices.md#creating-a-framework-usb-device-object)フレームワークは、デバイスの最初の USB 構成を含む USB インターフェイスごとに framework USB インターフェイス オブジェクトを作成します。

ほとんどの USB デバイスが 1 つだけのインターフェイスを持ち、インターフェイスが 1 つだけの代替設定には. このようなデバイス ドライバーは通常、フレームワークの USB インターフェイス オブジェクトを定義するオブジェクトのメソッドを使用する必要はありません。

ドライバーは、複数のインターフェイスまたは代替の設定を提供する USB デバイスをサポートする場合、インターフェイス オブジェクトのメソッドには、次の操作を実行するドライバーが有効にします。

-   [インターフェイスの情報を取得します。](#obtaining-interface-information)

-   [USB インターフェイスに代替設定を選択します。](#selecting-an-alternate-setting-for-a-usb-interface)

### <a href="" id="obtaining-interface-information"></a> インターフェイスの情報を取得します。

ドライバーが呼び出された後[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)、呼び出すことができます[ **WdfUsbTargetDeviceGetInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550092)にデバイスの USB インターフェイスの 1 つを表す framework USB インターフェイス オブジェクトを識別するハンドルを取得します。 ドライバーは、USB インターフェイスに関する情報を取得するため、USB インターフェイス オブジェクトを定義するいくつかのメソッドを呼び出すことができます。

ドライバー メソッドを呼び出せる次いつでも呼び出し後に[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428):

<a href="" id="---------wdfusbinterfacegetinterfacenumber--------"></a>[**WdfUsbInterfaceGetInterfaceNumber**](https://msdn.microsoft.com/library/windows/hardware/ff550065)  
USB インターフェイスのオブジェクトに関連付けられている USB インターフェイスの数を返します。

<a href="" id="---------wdfusbinterfacegetdescriptor--------"></a>[**WdfUsbInterfaceGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550060)  
USB インターフェイスの設定のいずれかに関連付けられているその USB インターフェイス記述子を取得します。

<a href="" id="---------wdfusbinterfacegetnumendpoints--------"></a>[**WdfUsbInterfaceGetNumEndpoints**](https://msdn.microsoft.com/library/windows/hardware/ff550068)  
USB インターフェイスの設定のいずれかに関連付けられているエンドポイントの数を返します。

<a href="" id="---------wdfusbinterfacegetendpointinformation--------"></a>[**WdfUsbInterfaceGetEndpointInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550063)  
エンドポイントとその関連するパイプに関する情報を取得します。

呼び出し後に、ドライバーは、次のメソッドを呼び出すことができます[ **WdfUsbTargetDeviceSelectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff550101):

<a href="" id="---------wdfusbinterfacegetconfiguredsettingindex--------"></a>[**WdfUsbInterfaceGetConfiguredSettingIndex**](https://msdn.microsoft.com/library/windows/hardware/ff550059)  
USB インターフェイスの現在選択されている別の設定を識別するインデックス値を返します。

<a href="" id="---------wdfusbinterfacegetnumconfiguredpipes--------"></a>[**WdfUsbInterfaceGetNumConfiguredPipes**](https://msdn.microsoft.com/library/windows/hardware/ff550066)  
指定された USB デバイスのインターフェイスが構成されているパイプの数を返します。

<a href="" id="---------wdfusbinterfacegetconfiguredpipe--------"></a>[**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)  
指定した USB デバイス インターフェイスとパイプ インデックスに関連付けられている framework パイプ オブジェクトのハンドルを返します。

### <a href="" id="selecting-an-alternate-setting-for-a-usb-interface"></a> USB インターフェイスの代替設定を選択します。

ドライバーが呼び出された後[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)、ドライバーが呼び出せる[ **WdfUsbInterfaceGetNumSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff550070)USB インターフェイスをサポートする代替の設定の数を取得します。

ドライバーが呼び出された後[ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101) USB デバイスの構成を選択するには、ドライバーを呼び出すことができます[ **WdfUsbInterfaceSelectSetting**](https://msdn.microsoft.com/library/windows/hardware/ff550073)構成の USB インターフェイスの 1 つの代替の設定を選択します。

デバイスの代替設定は、0 から始まる連続して番号する必要があります。

関連情報については、次を参照してください。 [USB インターフェイスで代替の設定を選択する方法](https://msdn.microsoft.com/library/windows/hardware/hh968309)します。

 

 





