---
title: NetAdapterCx の制限事項
description: NetAdapterCx の制限事項
ms.assetid: 2333F2D9-A369-4124-9365-ABC49E8B5595
keywords:
- ネットワーク アダプターの WDF クラスの拡張機能の制限事項、NetAdapterCx の制限事項、NetCx の制限事項
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21146fe5f8dc5301b1d2e07807f0328d69a9848d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375345"
---
# <a name="netadaptercx-limitations"></a>NetAdapterCx の制限事項

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このトピックでは、NetAdapterCx クライアント ドライバーを WDF 関数を呼び出す際の注意すべき注意事項について説明します。

|関数 | 説明 |
|-|-|
| [**WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035) | 既定で[ **NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)割り当てます`SDDL_DEVOBJ_SYS_ALL_ADM_RWX_WORLD_RW_RES_R`SDDL の既定値として。 制限の厳しい SDDL を指定する場合、アプリケーションをクエリの Oid をアダプターに送信することできない可能性があります。 |
|[**WdfDeviceInitSetFileObjectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff546107)| クライアント ドライバーを設定する必要がありますいない**WdfFileObjectWdfCanUseFsContext**で、 **FileObjectClass**のメンバー [WDF_FILEOBJECT_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff551319)します。 |
| [**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)、 [ **WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)、 [ **WdfDeviceInitSetDeviceType**](https://msdn.microsoft.com/library/windows/hardware/ff546090)、 [ **WdfDeviceInitSetCharacteristics**](https://msdn.microsoft.com/library/windows/hardware/ff546074)、 [ **WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)、 [ **WdfDeviceInitSetPowerPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546766) | [**NetAdapterDeviceInitConfig** ](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)クライアント ドライバーの代わりにこれらのルーチンを呼び出します。 クライアント ドライバーはこれら呼び出さないでください。
| [**WdfDeviceCreateDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff545935) | クライアント ドライバーを呼び出す場合[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)で、 **ReferenceString**パラメーターと等しい**NULL**、NDISデバイス インターフェイスへの送信 I/O 要求をインターセプトします。 この動作を回避するには、任意の参照文字列を指定します。
