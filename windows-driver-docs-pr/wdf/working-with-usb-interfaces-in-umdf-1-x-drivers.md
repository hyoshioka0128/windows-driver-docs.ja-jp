---
title: UMDF 1.x ドライバーでの USB インターフェイスの操作
description: UMDF 1.x ドライバーでの USB インターフェイスの操作
ms.assetid: fc25e3b2-1631-445e-9340-a8cc92c68733
keywords:
- UMDF WDK、USB インターフェイス
- ユーザーモードドライバーフレームワーク WDK、USB インターフェイス
- ユーザーモードドライバー WDK UMDF、USB インターフェイス
- USB インターフェイス WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9182e90910e774d9c66f87ff4095eb2b4d286795
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823516"
---
# <a name="working-with-usb-interfaces-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでの USB インターフェイスの操作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、各 USB インターフェイスをフレームワークの USB インターフェイスオブジェクトとして表します。 UMDF ドライバーがフレームワークの USB デバイスオブジェクトを作成すると、フレームワークは、デバイスがサポートする各 USB インターフェイスのフレームワークの USB インターフェイスオブジェクトを作成します。

ほとんどの USB デバイスにはインターフェイスが1つだけあり、インターフェイスには代替の設定が1つしかありません。 通常、このようなデバイスのドライバーは、フレームワークの USB インターフェイスオブジェクトが定義するオブジェクトメソッドを使用する必要はありません。

UMDF ドライバーが複数のインターフェイスまたは代替設定を提供する USB デバイスをサポートしている場合、インターフェイスオブジェクトのメソッドを使用すると、次のことを行うことができます。

-   [インターフェイス情報を取得](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers#obtaining-umdf-usb-interface-information)します。

-   [USB インターフェイスの別の設定を選択して](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers#selecting-an-alternate-setting-for-a-umdf-usb-interface)ください。

### <a name="obtaining-umdf-usb-interface-information"></a>UMDF USB インターフェイス情報の取得

UMDF ドライバーが[**IWDFUsbTargetFactory:: CreateUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)メソッドを呼び出して、umdf usb ターゲットデバイスオブジェクトを作成した後、ドライバーは[**IWDFUsbTargetDevice:: getnuminterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)メソッドを呼び出して usb インターフェイスの数を取得できます。デバイスでサポートされている。 次に、ドライバーは[**IWDFUsbTargetDevice:: RetrieveUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)メソッドを呼び出して、デバイスがサポートしている USB インターフェイスを公開する[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)インターフェイスへのポインターを取得できます。 次に、ドライバーは、各 USB インターフェイスオブジェクトが USB インターフェイスに関する情報を取得するために定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbinterface--getinterfacenumber"></a>[**IWDFUsbInterface::GetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacenumber)  
USB インターフェイスオブジェクトに関連付けられている USB インターフェイス番号を取得します。

<a href="" id="iwdfusbinterface--getinterfacedescriptor"></a>[**IWDFUsbInterface:: GetInterfaceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)  
USB インターフェイスの代替設定のいずれかに関連付けられている USB インターフェイス記述子を取得します。

<a href="" id="iwdfusbinterface--getnumendpoints"></a>[**IWDFUsbInterface:: GetNumEndPoints**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getnumendpoints)  
USB インターフェイスの代替設定の1つに関連付けられているエンドポイント (パイプとも呼ばれます) の数を取得します。

<a href="" id="iwdfusbinterface--getconfiguredsettingindex"></a>[**IWDFUsbInterface::GetConfiguredSettingIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getconfiguredsettingindex)  
USB インターフェイスに対して現在選択されている別の設定を識別するインデックス値を取得します。

<a href="" id="iwdfusbinterface--retrieveusbpipeobject"></a>[**IWDFUsbInterface::RetrieveUsbPipeObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-retrieveusbpipeobject)  
指定した USB デバイスインターフェイスとパイプインデックスに関連付けられているフレームワークパイプオブジェクトを公開する、 [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)インターフェイスへのポインターを取得します。

<a href="" id="iwdfusbinterface--getwinusbhandle"></a>[**IWDFUsbInterface:: GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)  
USB インターフェイスに関連付けられている WinUsb インターフェイスハンドルを取得します。

### <a name="selecting-an-alternate-setting-for-a-umdf-usb-interface"></a>UMDF USB インターフェイスの別の設定を選択する

UMDF ドライバーは、 [**IWDFUsbInterface:: SelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)メソッドを呼び出して、デバイスがサポートしているいずれかの USB インターフェイスに対して別の設定を選択できます。

デバイスの代替設定には、ゼロから始まる番号を連続して指定する必要があります。

**重要**   設定を選択すると、インターフェイスとエンドポイントに関するすべての情報が無効になります。 そのため、ドライバーはこの情報を再度取得する必要があります。 また、ドライバーは、以前に取得したすべての USB パイプオブジェクトを破棄して再作成する必要があります。

 

 

 





