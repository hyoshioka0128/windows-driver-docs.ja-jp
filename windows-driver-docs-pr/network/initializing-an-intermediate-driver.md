---
title: 中間ドライバーの初期化
description: 中間ドライバーの初期化
ms.assetid: cd4903f8-f522-403a-bec4-03ee7e82dcac
keywords:
- NDIS 中間ドライバ、WDK の初期化
- ドライバー WDK 中級レベルのネットワーク、初期化しています
- 中間ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f39bdea54c77f822487f6d77c6ceeccb44ed345
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572478"
---
# <a name="initializing-an-intermediate-driver"></a>中間ドライバーの初期化



NDIS 中間ドライバ レジスタその*MiniportXxx*関数とその*ProtocolXxx*関数のコンテキストでその[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 登録するその*MiniportXxx*関数、中間のドライバーを呼び出す必要があります、 [NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654) NDIS で関数を\_中間\_ドライバー フラグを設定します。 このフラグは、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造で、ドライバーが渡される*MiniportDriverCharacteristics*します。 登録するその*ProtocolXxx*関数、中間のドライバーを呼び出す必要があります、 [NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113) NDIS 中間ドライバーとしてドライバーが正常に登録されている場合に STATUS_SUCCESS、またはその同等の NDIS_STATUS_SUCCESS を返します。 DriverEntry 伝達することによって返されたエラー状態で初期化が失敗したかどうか、 **NdisXxx**関数またはカーネル モードのサポート ルーチンでは、によってドライバーいないは読み込まれません。 **DriverEntry**実行する必要があります。 つまり、同期的には、STATUS_PENDING またはその同等 NDIS_STATUS_PENDING を返すことはできません。

NDIS、中間のドライバーに登録する、 [DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)には、少なくとも、ルーチンがあります。

- 呼び出す、 [NdisMRegisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563654) 、NDIS_INTERMEDIATE_DRIVER フラグを設定すると、ドライバーの登録を持つ関数*MiniportXxx*関数。
- 呼び出す、 [NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数ドライバーの登録を*ProtocolXxx*場合と、ドライバー、その後バインド自体、基になる NDIS ドライバーに機能します。
- 呼び出す、 [NdisIMAssociateMiniport](https://msdn.microsoft.com/library/windows/hardware/ff562717) NDIS ドライバーのミニポートの上端と下端のプロトコル間の関連付けに通知する関数。

エラーが生じた場合**DriverEntry**後**NdisMRegisterMiniportDriver**ドライバーを呼び出す必要がありますが、正常に返さ、 [NdisMDeregisterMiniportDriver](https://msdn.microsoft.com/library/windows/hardware/ff563578)関数前に**DriverEntry**を返します。 場合**DriverEntry**成功すると、ドライバーを呼び出す必要があります**NdisMDeregisterMiniportDriver**からその[MiniportDriverUnload](https://msdn.microsoft.com/library/windows/hardware/ff559378)関数。

中間ドライバーの大部分を共有する、 **DriverEntry**プロトコルおよびミニポートのドライバーの要件。

中間のドライバーの仮想ミニポートの初期化は、ドライバーを呼び出すときに発生します。、 [NdisIMInitializeDeviceInstanceEx](https://msdn.microsoft.com/library/windows/hardware/ff562727)関数からその[ProtocolBindAdapterEx](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。

NDIS 呼び出し、 *ProtocolBindAdapterEx*ミニポート ドライバーをすべて基になる関数を初期化します。

実際には、 **DriverEntry** NDIS 中間のドライバーの機能を無視することができます、 *RegistryPath*ポインターに渡して後**NdisMRegisterMiniportDriver**します。 このようなドライバーが無視することも、 *DriverObject*ポインターに渡して後**NdisMRegisterMiniportDriver**します。 ただし、ドライバーが保存ミニポート ドライバーによって返されるハンドル値**NdisMRegisterMiniportDriver**で*NdisMiniportDriverHandle*とプロトコルのハンドル値によって返される**NdisRegisterProtocolDriver**で*NdisProtocolHandle*後続の呼び出しの**NdisXxx**関数。 中間のドライバーの*ProtocolBindAdapterEx*関数では、ドライバーをバインドする前に基になる各ミニポート ドライバーにその*MiniportInitializeEx*関数は、中間を初期化するために呼び出されます仮想ミニポートのドライバーの。 高いレベルのプロトコルのドライバーでは、作成した仮想ミニポートに自体、その後バインドします。 この戦略には、NDIS 中間ドライバーがバインドされている、基になるミニポート ドライバーの機能に従って仮想ミニポートの作成時のリソースを割り当てることができます。
