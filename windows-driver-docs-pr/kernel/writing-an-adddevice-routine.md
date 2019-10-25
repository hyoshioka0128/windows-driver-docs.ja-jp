---
title: AddDevice ルーチンの記述
description: AddDevice ルーチンの記述
ms.assetid: 93a272f4-888c-4cc8-b013-c6313c10a8d8
keywords:
- 標準ドライバールーチン WDK カーネル、AddDevice ルーチン
- ドライバールーチン WDK カーネル、AddDevice ルーチン
- ルーチン WDK カーネル、AddDevice ルーチン
- AddDevice ルーチン WDK カーネル
- システム領域のメモリ割り当て (WDK カーネル)
- システムリソースストレージ WDK カーネル
- システムリソースの格納
- デバイスオブジェクト WDK カーネル、作成
- デバイスの初期化 WDK カーネル
- デバイスの初期化
- AddDevice ルーチン WDK カーネル, AddDevice ルーチンについて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e06de0746a89551f61f37c65f9b4eef882c9d308
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838297"
---
# <a name="writing-an-adddevice-routine"></a>AddDevice ルーチンの記述





PnP をサポートするすべてのドライバーには、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが必要です。 *AddDevice*ルーチンは、ドライバーが i/o 要求を実行する物理デバイス、論理デバイス、または仮想デバイスを表す1つまたは複数のデバイスオブジェクトを作成します。 また、デバイスオブジェクトをデバイススタックにアタッチします。そのため、デバイススタックには、デバイスに関連付けられている各ドライバーのデバイスオブジェクトが格納されます。

PnP マネージャーは、ドライバーによって制御されるデバイスごとにドライバーの*AddDevice*ルーチンを呼び出します。 *AddDevice*ルーチンは、システムの初期化中に (デバイスが最初に列挙されたとき)、システムの実行中に新しいデバイスが列挙されるたびに呼び出されます。

このセクションでは、次のトピックについて説明します。

[関数またはフィルタードライバーの AddDevice ルーチン](adddevice-routines-in-function-or-filter-drivers.md)

[バスドライバーの AddDevice ルーチン](adddevice-routines-in-bus-drivers.md)

[AddDevice ルーチンの記述に関するガイドライン](guidelines-for-writing-adddevice-routines.md)

 

 




