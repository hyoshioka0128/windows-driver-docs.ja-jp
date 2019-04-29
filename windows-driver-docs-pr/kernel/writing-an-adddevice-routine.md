---
title: AddDevice ルーチンの記述
description: AddDevice ルーチンの記述
ms.assetid: 93a272f4-888c-4cc8-b013-c6313c10a8d8
keywords:
- 標準のドライバーのルーチンの WDK カーネル、AddDevice ルーチン
- ドライバーのルーチンの WDK カーネル、AddDevice ルーチン
- ルーチンの WDK カーネル、AddDevice ルーチン
- AddDevice ルーチン WDK カーネル
- システム容量のメモリ割り当ての WDK カーネル
- システム リソースのストレージの WDK カーネル
- システム リソースを格納します。
- デバイス オブジェクトの WDK カーネルを作成します。
- デバイスの初期化の WDK カーネル
- デバイスの初期化
- AddDevice ルーチンについて、AddDevice ルーチンの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 609ba2b2556e24f09b8335dce6cf8efad2ba5f59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384535"
---
# <a name="writing-an-adddevice-routine"></a>AddDevice ルーチンの記述





PnP をサポートする任意のドライバーが必要、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 *AddDevice*ルーチンは、ドライバーが I/O 要求を実行する物理、論理、または仮想デバイスを表す 1 つまたは複数のデバイス オブジェクトを作成します。 デバイス オブジェクトを添付、デバイス スタック デバイス スタックは、デバイスに関連付けられた各ドライバーのデバイス オブジェクトが含まれるようにします。

PnP マネージャーには、ドライバーの*AddDevice*ドライバーによって制御される各デバイスの日常的な。 *AddDevice*ルーチンは、システムの初期化 (デバイスが最初に列挙) の場合、中に呼び出され、いつでも、新しいデバイスは、システムの実行中に列挙されます。

このセクションでは、次のトピックについて説明します。

[関数またはフィルター ドライバーで AddDevice ルーチン](adddevice-routines-in-function-or-filter-drivers.md)

[バス ドライバー AddDevice ルーチン](adddevice-routines-in-bus-drivers.md)

[AddDevice ルーチンを記述するためのガイドライン](guidelines-for-writing-adddevice-routines.md)

 

 




