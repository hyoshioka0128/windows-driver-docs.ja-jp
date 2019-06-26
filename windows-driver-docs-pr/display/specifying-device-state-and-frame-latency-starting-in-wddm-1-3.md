---
title: WDDM 1.3 でのデバイスの状態およびフレームの待機時間の指定
ms.assetid: 97FC54BD-0D20-4235-B914-5F44690274AE
description: Windows 表示 Driver Model (WDDM) 1.3 以降は、ユーザー モードのディスプレイ ドライバーは、ディスプレイのミニポート ドライバーにデバイスの状態とフレームの待機時間に関する情報を渡すエスケープ フラグを使用できます。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 937114aca5fe1017617e4e36c4659837945fd28c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376072"
---
# <a name="specifying-device-state-and-frame-latency-in-wddm-13"></a>WDDM 1.3 でのデバイスの状態およびフレームの待機時間の指定


Windows 表示 Driver Model (WDDM) 1.3 以降は、ユーザー モードのディスプレイ ドライバーできますエスケープ フラグを使用して、ディスプレイのミニポート ドライバーにデバイスの状態とフレームの待機時間に関する情報を渡すときに、 [ *pfnEscapeCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)関数が呼び出されます。 これらのフラグが表示されます、 [ **D3DDDI\_ESCAPEFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags)構造では、Windows 8.1 を起動します。

これらの参照トピックには、ユーザー モードのディスプレイ ドライバーでこの機能を実装する方法について説明します。

-   [**D3DDDI\_DEVICEEXECUTION\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_deviceexecution_state)
-   [**D3DDDI\_EXECUTIONSTATEESCAPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_executionstateescape)
-   [**D3DDDI\_FRAMELATENCYESCAPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_framelatencyescape)
-   [**D3DDDI\_ESCAPEFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags) (新しい**DeviceStatusQuery**と**ChangeFrameLatency**メンバー)

 

 





