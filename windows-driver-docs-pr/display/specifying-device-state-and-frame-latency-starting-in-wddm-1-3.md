---
title: WDDM 1.3 でのデバイスの状態およびフレームの待機時間の指定
ms.assetid: 97FC54BD-0D20-4235-B914-5F44690274AE
description: Windows Display Driver Model (WDDM) 1.3 以降では、ユーザーモード表示ドライバーは、エスケープフラグを使用して、デバイスの状態とフレームの待機時間の情報をディスプレイミニポートドライバーに渡すことができます。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: cc2614e38aa873c10e55a58fb95ff8ce1d887285
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829445"
---
# <a name="specifying-device-state-and-frame-latency-in-wddm-13"></a>WDDM 1.3 でのデバイスの状態およびフレームの待機時間の指定


Windows Display Driver Model (WDDM) 1.3 以降では、ユーザーモードの表示ドライバーは、 [*pfnEscapeCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)関数が呼び出されたときに、エスケープフラグを使用してデバイスの状態とフレームの待機時間の情報をディスプレイミニポートドライバーに渡すことができます。 これらのフラグは、Windows 8.1 以降の[**D3DDDI\_ESCAPEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags)構造体で使用できます。

以下の参照トピックでは、ユーザーモードの表示ドライバーにこの機能を実装する方法について説明します。

-   [**D3DDDI\_DEVICEEXECUTION\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_deviceexecution_state)
-   [**D3DDDI\_EXECUTIONSTATEESCAPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_executionstateescape)
-   [**D3DDDI\_FRAMELATのエスケープ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_framelatencyescape)
-   [**D3DDDI\_ESCAPEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags) (新しい**devicestatusquery**と**changeframmembers** )

 

 





