---
title: AdapterControl ルーチンの記憶域の要件
description: AdapterControl ルーチンの記憶域の要件
ms.assetid: 5e5711df-9acd-4ac5-b6b2-4e90299afb24
keywords:
- AdapterControl ルーチン、storage
- AdapterControl ルーチン、書き込み
- アダプタオブジェクト WDK カーネル、AdapterControl ルーチンの記述
- DMA が WDK カーネルを転送し、AdapterControl ルーチンを作成する
- storage WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd27ba68c3dca1668cd9474e88a46f72e5ba051c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836231"
---
# <a name="storage-requirements-for-adaptercontrol-routines"></a>AdapterControl ルーチンの記憶域の要件





[*アダプターに Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンが含まれている場合、ドライバーは次のような常駐ストレージを提供する必要があります。

-   DMA 操作で使用されるコンテキスト情報

-   IoGetDmaAdapter によって返されるアダプターオブジェクトポインター [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

-   特定の DMA 転送要求で使用できるシステムによって決定された最大*Numberofmapregisters*を保持するための ULONG 型の変数

ドライバーは、デバイス拡張機能、コントローラー拡張機能、またはドライバーによって割り当てられた非ページプールで必要な記憶域を提供できます。

 

 




