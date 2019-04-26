---
title: KMDF ミニポート ドライバーの作成
description: KMDF ミニポート ドライバーの作成
ms.assetid: 3e01827b-fe1e-49ce-8072-9fc6c751fc01
keywords:
- ミニポート ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2253b9d48be2a68d6d055a0e89b5e0f43385df6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358552"
---
# <a name="creating-kmdf-miniport-drivers"></a>KMDF ミニポート ドライバーの作成





ポート/ミニポート アーキテクチャにより、ミニポート ドライバー WDM またはフレームワーク インターフェイスを使用して他のドライバーと通信する場合、一部のミニポート ドライバーはカーネル モード ドライバー フレームワークを使用できます。 たとえば、 [NDIS ミニポート ドライバー WDM が削減 edge](https://msdn.microsoft.com/library/windows/hardware/ff565954)フレームワークを使用して、下端を実装することができます。

ミニポート ドライバー、フレームワークを使用する場合は、ドライバーが必要です。

-   設定、 [ **WdfDriverInitNoDispatchOverride** ](https://msdn.microsoft.com/library/windows/hardware/ff551303)フラグ、 **DriverInitFlags**のドライバーのメンバー [ **WDF\_ドライバー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)呼び出す前に構造[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)します。 これにより、フラグを設定、ポート ドライバー、代わりに、フレームワークの I/O をインターセプトする要求パケット (Irp) I/O マネージャーがドライバーに指示しました。

-   呼び出す[ **WdfDeviceMiniportCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546802)の代わりに[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)フレームワーク、ミニポート ドライバーのデバイス オブジェクトを作成するにはデバイス。 ミニポート ドライバーを呼び出す必要があります**WdfDeviceMiniportCreate**ときにそのポート ドライバーを通知をデバイスが使用可能です。

-   呼び出す[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)デバイスでは削除するオブジェクトを[ **WdfDeviceMiniportCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546802)ドライバーを決定するときに、作成しますデバイスが削除されました。 (ドライバーが設定されているため、 [ **WdfDriverInitNoDispatchOverride** ](https://msdn.microsoft.com/library/windows/hardware/ff551303)フラグ、フレームワークは、デバイスが削除されたときを判断することはできず、デバイス オブジェクトを削除することはできません)。

-   呼び出す[ **WdfDriverMiniportUnload** ](https://msdn.microsoft.com/library/windows/hardware/ff547193)ときに、ポート用のドライバーにより、ミニポート ドライバーをアンロードするのには、します。

基になるデバイスは、プラグ アンド プレイ (PnP) をサポートしている場合にのみ、ミニポート ドライバーでは、フレームワークを使用できます。 ミニポート ドライバーでは、フレームワークのコントロールのデバイス オブジェクトを使用できません。

デバイス オブジェクトに制限が適用される、 [ **WdfDeviceMiniportCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546802)メソッドを作成します。 これらの制限事項の一覧は、次を参照してください。 [ **WdfDeviceMiniportCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546802)します。

 

 





