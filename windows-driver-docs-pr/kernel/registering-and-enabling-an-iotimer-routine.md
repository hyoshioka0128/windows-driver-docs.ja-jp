---
title: 登録して、IoTimer ルーチンを有効にします。
description: 登録して、IoTimer ルーチンを有効にします。
ms.assetid: d06a6430-5098-492a-8114-d6f390083718
keywords:
- IoTimer
- IoInitializeTimer
- IoStartTimer
- IoTimer ルーチンを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fb4440e38d71d6b799f6e1e8e3eedd74d724627
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529287"
---
# <a name="registering-and-enabling-an-iotimer-routine"></a>登録して、IoTimer ルーチンを有効にします。





すべてのドライバーが登録できる、 [ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)ルーチンを呼び出すことによって、1 つまたは複数のデバイス オブジェクトが作成された後[ **IoInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff549344)します。 ドライバーを呼び出してタイマーを開始できます[ **IoStartTimer**](https://msdn.microsoft.com/library/windows/hardware/ff550373)します。 次の図は、これらの呼び出しを示しています。

![iotimer ルーチンを使用して説明する図](images/3iotmer.png)

呼び出した後[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)デバイス オブジェクトを作成するドライバーを呼び出すことができます**IoInitializeTimer**のエントリ ポイントとその*IoTimer*日常的なデバイスのドライバーが作成したオブジェクトと、ドライバーがどのようなコンテキストを保持しますコンテキスト領域へのポインターと共にその*IoTimer*ルーチン。 I/O マネージャーは、タイマーのカーネルに割り当てられたオブジェクトをデバイス オブジェクトを関連付け、1 秒ごとにこのタイムアウト タイマー オブジェクトを設定します。

ドライバーの呼び出し後**IoStartTimer**その*IoTimer*ルーチンはドライバー呼び出されるまで 1 秒あたり 1 回呼び出されます[ **IoStopTimer**](https://msdn.microsoft.com/library/windows/hardware/ff550377)します。 ドライバーの呼び出しを再び有効にできる、 *IoTimer*ルーチン**IoStartTimer**します。 (多くの場合、ドライバーを呼び出すと**IoStartTimer**、現在の IRP の I/O スタックの場所から取得したデバイス オブジェクト ポインターを提供します)。

開始時、 *IoTimer*ルーチンには、デバイスのオブジェクト ポインターが渡された<em>、</em>ドライバーにはときに指定したコンテキストのポインターと共にと呼ばれる**IoInitializeTimer**。

ドライバーを呼び出してはならない**IoStopTimer**内から、 *IoTimer*ルーチン。

I/O マネージャーが、指定したデバイス オブジェクトのタイマーのルーチンの登録を解除し、ドライバーを呼び出すと、その関連付けられたコンテキストを解放[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)します。

 

 




