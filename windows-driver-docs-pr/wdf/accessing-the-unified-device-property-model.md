---
title: 統合デバイス プロパティ モデルへのアクセス
description: このトピックでは、Windows ドライバーフレームワーク (WDF) ドライバーが、統合されたデバイスプロパティモデルを通じて公開されるプロパティを取得または変更する方法について説明します。
ms.assetid: C81988F9-E0DA-439F-B770-DAD86E33D5F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 041a1aeb18f417948d6ce3a611802e9217b83aa0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845513"
---
# <a name="accessing-the-unified-device-property-model"></a>統合デバイス プロパティ モデルへのアクセス


このトピックでは、Windows ドライバーフレームワーク (WDF) ドライバーが、統合されたデバイスプロパティモデルを通じて公開されるプロパティを取得または変更する方法について説明します。 一覧表示されているメソッドは、ユーザーモードドライバーフレームワーク (UMDF) バージョン2.0 およびカーネルモードドライバーフレームワーク (KMDF) バージョン1.13 から使用できます。

KMDF と UMDF の両方のドライバーで、次のメソッドを呼び出すことができます。

-   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
-   [**Wdfdevice割り当てプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
-   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)

KMDF と UMDF ドライバーはどちらも、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出す前に、次のメソッドを呼び出すことができます。 **WdfDeviceCreate**の呼び出しの詳細については、「[フレームワークデバイスオブジェクトの作成](creating-a-framework-device-object.md)」を参照してください。

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出した後、ドライバーは対応する**Wdfdevice*Xxx*プロパティ**メソッドを呼び出すことによって、デバイスのプロパティ情報を取得できます。

-   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
-   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

上記の *-ex*メソッドは、 [**WDF\_デバイス\_プロパティ\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_property_data)構造体を使用してプロパティを指定できるという*点で、非対応の*メソッドとは異なります。これは、を使用して[**指定できるサブセットではありません。DEVICE\_REGISTRY\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ne-wudfwdm-device_registry_property)。

デバイスプロパティデータを受け取る前に、ドライバーは通常、必要なバッファーサイズを取得するためだけに**Wdf*Xxx*queryproperty**を呼び出します。 プロパティによっては、必要なサイズが返されたときと、ドライバーが**Wdf*Xxx*queryproperty**を再度呼び出すときのデータサイズが変わることがあります。 したがって、ドライバーは、戻り値の状態が [\_状態] ではない場合に実行されるループ内で**Wdf*Xxx*queryproperty**を呼び出す必要があります。 **\_は\_小さすぎ**ます。

必要なバッファーサイズが既知で不変である場合にのみ、 **Wdf*xxx*queryproperty**を使用することをお勧めします。この場合、ドライバーは**Wdf*Xxx*queryproperty**を1回だけ呼び出す必要があるからです。 必要なバッファーサイズが不明または異なる場合、ドライバーは**Wdf*Xxx*allocandqueryproperty**を呼び出す必要があります。

## <a name="accessing-device-interface-properties"></a>デバイス インターフェイス プロパティへのアクセス


UMDF ドライバーでは、次のメソッドを使用して、統合プロパティモデルを通じて公開されている[デバイスインターフェイスのプロパティ](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))を取得または変更できます。

-   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
-   [**Wdfdevice割り当て Interfaceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
-   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)

デバイスインターフェイスプロパティを取得または変更するには、KMDF ドライバーが[**Iogetdeviceinterfacepropertydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfacepropertydata)または[**iogetdeviceinterfacepropertydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacepropertydata)を直接呼び出す必要があります。

 

 





