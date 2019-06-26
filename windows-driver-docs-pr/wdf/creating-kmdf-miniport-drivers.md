---
title: KMDF ミニポート ドライバーの作成
description: KMDF ミニポート ドライバーの作成
ms.assetid: 3e01827b-fe1e-49ce-8072-9fc6c751fc01
keywords:
- ミニポート ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f3f9f6df417eec2488976f1f299e43f7f50ffa1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377496"
---
# <a name="creating-kmdf-miniport-drivers"></a>KMDF ミニポート ドライバーの作成





ポート/ミニポート アーキテクチャにより、ミニポート ドライバー WDM またはフレームワーク インターフェイスを使用して他のドライバーと通信する場合、一部のミニポート ドライバーはカーネル モード ドライバー フレームワークを使用できます。 たとえば、 [NDIS ミニポート ドライバー WDM が削減 edge](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-miniport-drivers-with-a-wdm-lower-edge)フレームワークを使用して、下端を実装することができます。

ミニポート ドライバー、フレームワークを使用する場合は、ドライバーが必要です。

-   設定、 [ **WdfDriverInitNoDispatchOverride** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)フラグ、 **DriverInitFlags**のドライバーのメンバー [ **WDF\_ドライバー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)呼び出す前に構造[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)します。 これにより、フラグを設定、ポート ドライバー、代わりに、フレームワークの I/O をインターセプトする要求パケット (Irp) I/O マネージャーがドライバーに指示しました。

-   呼び出す[ **WdfDeviceMiniportCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)の代わりに[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)フレームワーク、ミニポート ドライバーのデバイス オブジェクトを作成するにはデバイス。 ミニポート ドライバーを呼び出す必要があります**WdfDeviceMiniportCreate**ときにそのポート ドライバーを通知をデバイスが使用可能です。

-   呼び出す[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)デバイスでは削除するオブジェクトを[ **WdfDeviceMiniportCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)ドライバーを決定するときに、作成しますデバイスが削除されました。 (ドライバーが設定されているため、 [ **WdfDriverInitNoDispatchOverride** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)フラグ、フレームワークは、デバイスが削除されたときを判断することはできず、デバイス オブジェクトを削除することはできません)。

-   呼び出す[ **WdfDriverMiniportUnload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdriverminiportunload)ときに、ポート用のドライバーにより、ミニポート ドライバーをアンロードするのには、します。

基になるデバイスは、プラグ アンド プレイ (PnP) をサポートしている場合にのみ、ミニポート ドライバーでは、フレームワークを使用できます。 ミニポート ドライバーでは、フレームワークのコントロールのデバイス オブジェクトを使用できません。

デバイス オブジェクトに制限が適用される、 [ **WdfDeviceMiniportCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)メソッドを作成します。 これらの制限事項の一覧は、次を参照してください。 [ **WdfDeviceMiniportCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)します。

 

 





