---
title: NetAdapterCx の制限事項
description: NetAdapterCx の制限事項
ms.assetid: 2333F2D9-A369-4124-9365-ABC49E8B5595
keywords:
- ネットワーク アダプターの WDF クラスの拡張機能の制限事項、NetAdapterCx の制限事項、NetCx の制限事項
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a2d3c13a895607ccfc56399f385c9878728c79f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382823"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx の制限事項

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このトピックでは、NetAdapterCx クライアント ドライバーを WDF 関数を呼び出す際の注意すべき注意事項について説明します。

|関数 | 説明 |
|-|-|
| [**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) | 既定で[ **NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)割り当てます`SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R`SDDL の既定値として。 制限の厳しい SDDL を指定する場合、アプリケーションをクエリの Oid をアダプターに送信することできない可能性があります。 |
|[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)| クライアント ドライバーを設定する必要がありますいない**WdfFileObjectWdfCanUseFsContext**で、 **FileObjectClass**のメンバー [WDF_FILEOBJECT_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)します。 |
| [**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)、 [ **WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)、 [ **WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)、 [ **WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)、 [ **WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)、 [ **WdfDeviceInitSetPowerPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) | [**NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)クライアント ドライバーの代わりにこれらのルーチンを呼び出します。 クライアント ドライバーはこれら呼び出さないでください。
| [**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) | クライアント ドライバーを呼び出す場合[ **WdfDeviceCreateDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)で、 **ReferenceString**パラメーターと等しい**NULL**、NDISデバイス インターフェイスへの送信 I/O 要求をインターセプトします。 この動作を回避するには、任意の参照文字列を指定します。
