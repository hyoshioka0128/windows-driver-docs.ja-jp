---
title: AddDevice、ルーチンを記述します。
description: AddDevice、ルーチンを記述します。
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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530246"
---
# <a name="writing-an-adddevice-routine"></a>AddDevice、ルーチンを記述します。





PnP をサポートする任意のドライバーが必要、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 *AddDevice*ルーチンは、ドライバーが I/O 要求を実行する物理、論理、または仮想デバイスを表す 1 つまたは複数のデバイス オブジェクトを作成します。 デバイス オブジェクトを添付、デバイス スタック デバイス スタックは、デバイスに関連付けられた各ドライバーのデバイス オブジェクトが含まれるようにします。

PnP マネージャーには、ドライバーの*AddDevice*ドライバーによって制御される各デバイスの日常的な。 *AddDevice*ルーチンは、システムの初期化 (デバイスが最初に列挙) の場合、中に呼び出され、いつでも、新しいデバイスは、システムの実行中に列挙されます。

このセクションには、次のトピックが含まれています。

[関数またはフィルター ドライバーで AddDevice ルーチン](adddevice-routines-in-function-or-filter-drivers.md)

[バス ドライバー AddDevice ルーチン](adddevice-routines-in-bus-drivers.md)

[AddDevice ルーチンを記述するためのガイドライン](guidelines-for-writing-adddevice-routines.md)

 

 




