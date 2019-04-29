---
title: WDDM 1.3 でのデバイスの状態およびフレームの待機時間の指定
ms.assetid: 97FC54BD-0D20-4235-B914-5F44690274AE
description: Windows 表示 Driver Model (WDDM) 1.3 以降は、ユーザー モードのディスプレイ ドライバーは、ディスプレイのミニポート ドライバーにデバイスの状態とフレームの待機時間に関する情報を渡すエスケープ フラグを使用できます。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3254cb07f8e14b3dd70006b0e8b071eec6256520
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389978"
---
# <a name="specifying-device-state-and-frame-latency-in-wddm-13"></a>WDDM 1.3 でのデバイスの状態およびフレームの待機時間の指定


Windows 表示 Driver Model (WDDM) 1.3 以降は、ユーザー モードのディスプレイ ドライバーできますエスケープ フラグを使用して、ディスプレイのミニポート ドライバーにデバイスの状態とフレームの待機時間に関する情報を渡すときに、 [ *pfnEscapeCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568908)関数が呼び出されます。 これらのフラグが表示されます、 [ **D3DDDI\_ESCAPEFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544541)構造では、Windows 8.1 を起動します。

これらの参照トピックには、ユーザー モードのディスプレイ ドライバーでこの機能を実装する方法について説明します。

-   [**D3DDDI\_DEVICEEXECUTION\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn482416)
-   [**D3DDDI\_EXECUTIONSTATEESCAPE**](https://msdn.microsoft.com/library/windows/hardware/dn482417)
-   [**D3DDDI\_FRAMELATENCYESCAPE**](https://msdn.microsoft.com/library/windows/hardware/dn482418)
-   [**D3DDDI\_ESCAPEFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544541) (新しい**DeviceStatusQuery**と**ChangeFrameLatency**メンバー)

 

 





