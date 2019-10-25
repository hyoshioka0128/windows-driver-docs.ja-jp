---
title: KMDF ミニポート ドライバーの作成
description: KMDF ミニポート ドライバーの作成
ms.assetid: 3e01827b-fe1e-49ce-8072-9fc6c751fc01
keywords:
- ミニポートドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad5605ffd6441cd9cab9d6ee05c80f65a2db840
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844679"
---
# <a name="creating-kmdf-miniport-drivers"></a>KMDF ミニポート ドライバーの作成





ポート/ミニポートアーキテクチャによって、ミニポートドライバーが WDM またはフレームワークインターフェイスを使用して他のドライバーと通信できる場合は、一部のミニポートドライバーでカーネルモードドライバーフレームワークを使用できます。 たとえば、 [WDM が低い状態の NDIS ミニポートドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-miniport-drivers-with-a-wdm-lower-edge)は、フレームワークを使用して下端を実装できます。

ミニポートドライバーでフレームワークを使用する場合、ドライバーは次のことを行う必要があります。

-   [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出す前に、ドライバーの[**WDF\_driver\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体の**Driverinitflags**メンバーに[**WdfDriverInitNoDispatchOverride**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)フラグを設定します。 このフラグを設定すると、i/o マネージャーがドライバーに転送した i/o 要求パケット (Irp) を、フレームワークではなくポートドライバーでインターセプトできます。

-   [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)の代わりに[**WdfDeviceMiniportCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)を呼び出して、ミニポートドライバーのデバイス用のフレームワークデバイスオブジェクトを作成します。 ミニポートドライバーは、デバイスが使用可能であることをポートドライバーが通知するときに**WdfDeviceMiniportCreate**を呼び出す必要があります。

-   [**WdfDeviceMiniportCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)によって作成されたデバイスオブジェクトを削除するには、 [**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出します。デバイスが削除されたことがドライバーによって判断された場合。 (ドライバーによって[**WdfDriverInitNoDispatchOverride**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)フラグが設定されているため、デバイスがいつ削除され、デバイスオブジェクトを削除できないかは、フレームワークによって判断できません)。

-   ポートドライバーが、ミニポートドライバーがアンロードされようとしていることを通知するときに、 [**Wdfdriverminiportunload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdriverminiportunload)を呼び出します。

ミニポートドライバーは、基になるデバイスがプラグアンドプレイ (PnP) をサポートしている場合にのみ、フレームワークを使用できます。 ミニポートドライバーは、フレームワークのコントロールデバイスオブジェクトを使用できません。

[**WdfDeviceMiniportCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)メソッドによって作成されるデバイスオブジェクトに制限が適用されます。 これらの制限の一覧については、「 [**WdfDeviceMiniportCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)」を参照してください。

 

 





