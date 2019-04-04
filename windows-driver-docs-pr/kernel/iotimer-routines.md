---
title: IoTimer ルーチン
description: IoTimer ルーチン
ms.assetid: bc69c7b5-ce63-435e-b5b4-0d65ee153d31
keywords:
- 同期の WDK カーネル、タイマー
- IoTimer
- デバイスのタイムアウトの WDK カーネル
- タイムアウトの WDK カーネル
- タイミング操作 WDK カーネル
- タイムアウトのデバイスの I/O 操作の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c3ad5b26b6efa779b70582c7106dab9b1964c8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556833"
---
# <a name="iotimer-routines"></a>IoTimer ルーチン





判断 (カウンター) などのドライバーの定義の変数を更新するか、どの短い時間の間隔で必須ではありませんすべての操作にかかる時間をデバイスの操作がタイムアウトしてかどうかに、定期的に呼び出される必要のあるドライバーを使用できます、 [ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)ルーチン。 *IoTimer*ルーチンは、DPC ルーチンでは実際には、I/O マネージャーが 1 秒あたり 1 回呼び出し、デバイス オブジェクトに関連付けられています。 ドライバーが持つことができます、 *IoTimer*ルーチンが作成する各デバイス オブジェクトにします。

一般に、ドライバーを使用する必要があります、 *IoTimer*ルーチンを 1 秒間の一定の間隔を必要とする時の操作をします。 変数を必要とする時の操作を間隔または毎秒 1 回よりも短い間隔では、ドライバーは、タイマー オブジェクトを割り当てる必要があります。 詳細については、[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)を参照してください。

このセクションには、次のトピックが含まれています。

[登録して、IoTimer ルーチンを有効にします。](registering-and-enabling-an-iotimer-routine.md)

[IoTimer コンテキスト情報を提供します。](providing-iotimer-context-information.md)

[IoTimer ルーチンを使用します。](using-an-iotimer-routine.md)

 

 




