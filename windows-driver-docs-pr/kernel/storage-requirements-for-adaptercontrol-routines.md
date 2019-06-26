---
title: AdapterControl ルーチンの記憶域の要件
description: AdapterControl ルーチンの記憶域の要件
ms.assetid: 5e5711df-9acd-4ac5-b6b2-4e90299afb24
keywords:
- AdapterControl ルーチンでは、ストレージ
- 書き込みの AdapterControl ルーチン
- アダプター オブジェクトの WDK カーネル、AdapterControl ルーチンを記述
- AdapterControl ルーチンを記述、DMA 転送 WDK カーネル
- 記憶域 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb3266a369cb1f15d33b0b1654536bd742a3da7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382975"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl ルーチンの記憶域の要件





ある場合、 [ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control) 、日常的なドライバーをする必要があります常駐記憶域の提供次。

-   DMA 操作で使用されるコンテキスト情報

-   によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)

-   システムにより決定された最大値を保持する ULONG 型変数*NumberOfMapRegisters*あらゆる DMA 転送要求に対して使用可能な

ドライバーは、デバイスの拡張機能、コント ローラーの拡張機能、または、ドライバーによって割り当てられた非ページ プールのために必要な記憶域を提供できます。

 

 




