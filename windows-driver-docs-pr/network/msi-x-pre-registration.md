---
title: MSI-X の事前登録
description: MSI-X の事前登録
ms.assetid: 93a09ebd-8a50-4c96-a926-54bb4686a618
keywords:
- MSI X の WDK ネットワーク、リソース要件をフィルター処理関数
- メッセージ シグナル割り込み WDK ネットワーク、リソース要件フィルター関数
- Msi WDK ネットワーク、リソース要件フィルター関数
- リソース要件関数 net WDK をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf46946b8d5258894f1b6aca5093d41a06c4af65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382638"
---
# <a name="msi-x-pre-registration"></a>MSI-X の事前登録





MSI X の変更の割り込みアフィニティをサポートするために、またはメッセージの割り込みのリソースを削除するには、ミニポート ドライバーは、リソース要件フィルター関数を確立する必要があります。 NDIS 呼び出される前にこの事前登録手順が発生した、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

リソース要件フィルター関数を確立するために、ミニポート ドライバーを提供する必要があります、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数。 ミニポート ドライバーを呼び出すと、 [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)関数を[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン、ドライバーエントリ ポイントを渡して*MiniportSetOptions*で、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造体。 NDIS 呼び出し、 *MiniportSetOptions*関数のコンテキストで**NdisMRegisterMiniportDriver**します。

*MiniportSetOptions*、ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を指定します、 [ **NDIS\_ミニポート\_PNP\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566475)構造体。 この構造体のエントリ ポイントを定義する、 [ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332)、 [ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)、 [ *MiniportStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559452)、および[ *MiniportFilterResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff559384)関数。

NDIS NDIS は、プラグ アンド プレイ (PnP) マネージャーから、デバイスの追加要求を受け取る、呼び出し、ミニポート ドライバーの*MiniportAddDevice*関数。 NDIS からに渡されるハンドル*MiniportAddDevice*で、 *MiniportAdapterHandle*パラメーターは、NDIS は後でに渡されるハンドル、 [ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

[ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332)、ドライバーの初期化、 [ **NDIS\_ミニポート\_追加\_デバイス\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565945)構造体し、この構造体を渡す、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。 NDIS\_ミニポート\_追加\_デバイス\_登録\_属性の構造に含まれる、 **MiniportAddDeviceContext**ミニポートを識別するハンドルは、メンバーデバイスのドライバーに割り当てられたコンテキストの領域。 NDIS は後でこのコンテキストのハンドルを提供します、 [ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)、 [ *MiniportFilterResourceRequirements*](https://msdn.microsoft.com/library/windows/hardware/ff559384)、 [*MiniportStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559452)、および[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 *MiniportInitializeEx*、コンテキスト ハンドルが渡された、 **MiniportAddDeviceContext**のメンバー、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)構造体、 *MiniportInitParameters*パラメーターを指します。

NDIS 後[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)と*MiniportAddDevice*返します NDIS\_状態\_成功すると、NDIS 呼び出し、 *MiniportFilterResourceRequirements*関数を受信するたびに、 [ **IRP\_MN\_フィルター\_リソース\_要件** ](https://msdn.microsoft.com/library/windows/hardware/ff550874) I/O 要求パケット (IRP)。 *MiniportFilterResourceRequirements* MSI X メッセージごとに割り込みアフィニティを変更する、メッセージの割り込みのリソースを追加またはドライバーは行ベースでの割り込みを登録している場合は、メッセージの割り込みリソースを削除、 [*MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 割り込みアフィニティのポリシーを設定する方法についての詳細については、次を参照してください。 [MSI X リソース フィルター](msi-x-resource-filtering.md)します。

NDIS は、PnP マネージャーからデバイスの削除要求を受け取る、NDIS 呼び出し、ミニポート ドライバーの[ *MiniportRemoveDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559427)関数。 *MiniportRemoveDevice*関数は、操作を取り消す必要がありますが、 [ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)関数を実行します。

 

 





