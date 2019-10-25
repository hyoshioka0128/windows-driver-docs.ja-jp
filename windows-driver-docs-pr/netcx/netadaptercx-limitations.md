---
title: NetAdapterCx の制限事項
description: NetAdapterCx の制限事項
ms.assetid: 2333F2D9-A369-4124-9365-ABC49E8B5595
keywords:
- ネットワークアダプター WDF クラス拡張の制限事項、NetAdapterCx の制限事項、NetCx の制限事項
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a212140224eeae6fee57e5c48728030574e6ba0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835511"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx の制限事項

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このトピックでは、NetAdapterCx クライアントドライバーから WDF functions を呼び出すときに注意する必要がある注意事項について説明します。

|関数 | 説明 |
|-|-|
| [**Wdfdeviceinit割り当て Sddlstring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) | 既定では、 [**NetAdapterDeviceInitConfig**](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig)によって `SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R` が既定の SDDL として割り当てられます。 より制限の緩い SDDL を指定すると、アプリケーションはクエリ Oid をアダプターに送信できなくなる可能性があります。 |
|[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)| クライアントドライバーは、 [WDF_FILEOBJECT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)の**fileobjectclass**メンバーで、 **Wdffile Twdfcanusefscontext**を設定しないでください。 |
| [**Wdfdeviceinit割り当て name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)、 [**WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)、 [**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)、 [**wdfdeviceinitassignname**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)、 [**wdfdeviceinitsetiotype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)、 [**WdfDeviceInitSetPowerPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)可能 | [**NetAdapterDeviceInitConfig**](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig)は、クライアントドライバーに代わってこれらのルーチンを呼び出します。 クライアントドライバーは、これらを呼び出すことはできません。
| [**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) | クライアントドライバーが、 **Referencestring**パラメーターが**NULL**に等しい[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)を呼び出すと、NDIS はデバイスインターフェイスに送信された i/o 要求をインターセプトします。 この動作を回避するには、任意の参照文字列を指定します。
