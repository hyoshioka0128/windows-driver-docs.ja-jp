---
title: UMDF 1.x ドライバーでの USB インターフェイスの操作
description: UMDF 1.x ドライバーでの USB インターフェイスの操作
ms.assetid: fc25e3b2-1631-445e-9340-a8cc92c68733
keywords:
- UMDF WDK、USB インターフェイス
- ユーザー モード ドライバー フレームワーク WDK、USB インターフェイス
- ユーザー モード ドライバー WDK UMDF、USB インターフェイス
- USB インターフェイス WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837a1c1b7de9be46dca929cbf9119676c3eabb53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355913"
---
# <a name="working-with-usb-interfaces-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでの USB インターフェイスの操作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、フレームワークの USB インターフェイス オブジェクトとして各 USB インターフェイスを表します。 UMDF ドライバー フレームワークの USB デバイス オブジェクトを作成する場合、フレームワークは、デバイスをサポートする USB インターフェイスごとには、framework USB インターフェイス オブジェクトを作成します。

ほとんどの USB デバイスが 1 つだけのインターフェイスを持ち、インターフェイスが 1 つだけの代替設定には. このようなデバイス ドライバーは通常、フレームワークの USB インターフェイス オブジェクトを定義するオブジェクトのメソッドを使用する必要はありません。

UMDF ドライバーでは、複数のインターフェイスまたは代替の設定を提供する USB デバイスをサポートする場合、インターフェイス オブジェクトのメソッドには、ドライバーが有効にします。

-   [インターフェイスの情報を取得](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers#obtaining-umdf-usb-interface-information)します。

-   [USB インターフェイスの別の設定を選択](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers#selecting-an-alternate-setting-for-a-umdf-usb-interface)します。

### <a name="obtaining-umdf-usb-interface-information"></a>UMDF USB インターフェイスの情報を取得します。

後、UMDF ドライバーが呼び出されて、 [ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice) UMDF USB ターゲット デバイス オブジェクト、ドライバーを作成するメソッドを呼び出すことができます、 [ **IWDFUsbTargetDevice::GetNumInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)デバイスをサポートする USB インターフェイスの数を取得します。 次に、ドライバーがへの呼び出しを行うことができます、 [ **IWDFUsbTargetDevice::RetrieveUsbInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)へのポインターを取得するメソッド、 [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)インターフェイスを公開する、USB デバイスをサポートするインターフェイス。 ドライバーは、USB インターフェイスに関する情報を取得するため各 USB インターフェイス オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbinterface--getinterfacenumber"></a>[**IWDFUsbInterface::GetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacenumber)  
USB インターフェイスのオブジェクトに関連付けられている USB インターフェイスの数を取得します。

<a href="" id="iwdfusbinterface--getinterfacedescriptor"></a>[**IWDFUsbInterface::GetInterfaceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)  
USB インターフェイスの設定のいずれかに関連付けられているその USB インターフェイス記述子を取得します。

<a href="" id="iwdfusbinterface--getnumendpoints"></a>[**IWDFUsbInterface::GetNumEndPoints**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getnumendpoints)  
USB インターフェイスの設定のいずれかに関連付けられているエンドポイント (パイプとも呼ばれます) の数を取得します。

<a href="" id="iwdfusbinterface--getconfiguredsettingindex"></a>[**IWDFUsbInterface::GetConfiguredSettingIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)  
USB インターフェイスの現在選択されている別の設定を識別するインデックス値を取得します。

<a href="" id="iwdfusbinterface--retrieveusbpipeobject"></a>[**IWDFUsbInterface::RetrieveUsbPipeObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject)  
ポインターを取得、 [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)指定した USB デバイス インターフェイスとパイプ インデックスに関連付けられている framework パイプ オブジェクトを公開するインターフェイス。

<a href="" id="iwdfusbinterface--getwinusbhandle"></a>[**IWDFUsbInterface::GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)  
USB インターフェイスに関連付けられている WinUsb インターフェイスのハンドルを取得します。

### <a name="selecting-an-alternate-setting-for-a-umdf-usb-interface"></a>UMDF USB インターフェイスの代替設定を選択します。

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbInterface::SelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)デバイスを USB のいずれかのインターフェイスの代替の設定を選択するメソッドをサポートしています。

デバイスの代替設定は、0 から始まる連続して番号する必要があります。

**重要な**  インターフェイスとエンドポイントに関する情報を無効にする設定を選択します。 そのため、ドライバーでは、再度この情報を取得する必要があります。 ドライバーは、取得したすべての USB パイプ オブジェクトの破棄し、再作成する必要がありますも。

 

 

 





