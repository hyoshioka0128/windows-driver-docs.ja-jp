---
title: NetAdapterCx の制限事項
description: NetAdapterCx の制限事項
ms.assetid: 2333F2D9-A369-4124-9365-ABC49E8B5595
keywords:
- ネットワークアダプター WDF クラス拡張の制限事項、NetAdapterCx の制限事項、NetCx の制限事項
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18e9f5b76d9ebe5033d8f78ab7e408e04e02b438
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209032"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx の制限事項

このトピックでは、NetAdapterCx クライアントドライバーから WDF functions を呼び出すときに注意する必要がある注意事項について説明します。

|関数 | 説明 |
|-|-|
| [**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) | 既定では、 [**NetAdapterDeviceInitConfig**](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig)によって `SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R` が既定の SDDL として割り当てられます。 より制限の緩い SDDL を指定すると、アプリケーションはクエリ Oid をアダプターに送信できなくなる可能性があります。 |
|[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)| クライアントドライバーは、 [WDF_FILEOBJECT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)の**fileobjectclass**メンバーで、 **Wdffileを Twdfcanusefscontext**を設定することはできません。 |
| [**WdfdeviceinitWdfDeviceInitSetReleaseHardwareOrderOnFailure name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)、 [****](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)、 [**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)、 [**wdfdeviceinitassignname**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)、 [**wdfdeviceinitsetiotype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)、 [**wdfdeviceinitsetpowerページング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)可能 | [**NetAdapterDeviceInitConfig**](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig)は、クライアントドライバーに代わってこれらのルーチンを呼び出します。 クライアントドライバーは、これらを呼び出すことはできません。
| [**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) | クライアントドライバーが、 **Referencestring**パラメーターが**NULL**に等しい[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)を呼び出すと、NDIS はデバイスインターフェイスに送信された i/o 要求をインターセプトします。 この動作を回避するには、任意の参照文字列を指定します。
