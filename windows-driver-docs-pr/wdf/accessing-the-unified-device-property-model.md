---
title: 統合デバイス プロパティ モデルへのアクセス
description: このトピックでは、Windows Driver Frameworks (WDF) ドライバーを取得する方法について説明します。 または、統一されたデバイス プロパティのモデルで公開されているプロパティを変更します。
ms.assetid: C81988F9-E0DA-439F-B770-DAD86E33D5F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ae5f6d8211f5dc16867b75e9b29fe45043b3a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379054"
---
# <a name="accessing-the-unified-device-property-model"></a>統合デバイス プロパティ モデルへのアクセス


このトピックでは、Windows Driver Frameworks (WDF) ドライバーを取得する方法について説明します。 または、統一されたデバイス プロパティのモデルで公開されているプロパティを変更します。 メソッドの一覧は、ユーザー モード ドライバー フレームワーク (UMDF) version 2.0 とカーネル モード ドライバー フレームワーク (KMDF) バージョン 1.13 から利用可能です。

KMDF と UMDF ドライバーでは、次のメソッドを呼び出すことができます。

-   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
-   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
-   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)

KMDF と UMDF ドライバーは、次のメソッドを呼び出す前にのみ呼び出すことができます[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。 呼び出し元の詳細については**WdfDeviceCreate**を参照してください[Framework デバイス オブジェクトを作成する](creating-a-framework-device-object.md)します。

呼び出した後[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)、ドライバーは、デバイス プロパティ情報を入手して、対応する**WdfDevice*Xxx*プロパティ**メソッド。

-   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
-   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

*、Ex*上記のメソッドは、自分以外のとは異なる *、Ex*に対応することができるを使用してプロパティを指定、 [ **WDF\_デバイス\_プロパティ\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_property_data)構造体のサブセットを使用して指定できるのではなく、 [**デバイス\_レジストリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ne-wudfwdm-device_registry_property).

ドライバー デバイス プロパティのデータを受信する前に呼び出す通常**Wdf*Xxx*QueryProperty**必要なバッファー サイズを取得するだけです。 必要なサイズが返され、ドライバーを呼び出すとの間、一部のプロパティのデータのサイズを変更できます**Wdf*Xxx*QueryProperty**もう一度です。 そのため、ドライバーを呼び出す必要があります**Wdf*Xxx*QueryProperty**戻り値の状態が解除されるまでに実行されるループ内で**状態\_バッファー\_すぎます\_小さな**します。

使用することをお勧め**Wdf*Xxx*QueryProperty**を呼び出す、ドライバーがそうであるため、必要なバッファー サイズが、明白場合にのみ**Wdf*Xxx*QueryProperty** 1 回だけです。 必要なバッファー サイズが不明かによって異なります場合、ドライバーを呼び出す必要があります**Wdf*Xxx*AllocAndQueryProperty**します。

## <a name="accessing-device-interface-properties"></a>デバイス インターフェイス プロパティへのアクセス


UMDF ドライバーは、次のメソッドを使用して、取得したり変更したり[デバイス インターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))統一されたプロパティのモデルで公開されます。

-   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
-   [**WdfDeviceAssignInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
-   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)

取得したり、デバイス インターフェイスのプロパティを変更したりするには、KMDF ドライバーを呼び出す必要があります[ **IoGetDeviceInterfacePropertyData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfacepropertydata)または[ **IoSetDeviceInterfacePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacepropertydata)直接します。

 

 





