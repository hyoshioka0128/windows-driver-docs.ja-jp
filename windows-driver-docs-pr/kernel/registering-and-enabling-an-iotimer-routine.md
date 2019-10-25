---
title: IoTimer ルーチンの登録と有効化
description: IoTimer ルーチンの登録と有効化
ms.assetid: d06a6430-5098-492a-8114-d6f390083718
keywords:
- IoTimer
- IoInitializeTimer
- IoStartTimer
- IoTimer ルーチンを登録しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8ebb185831571dafbb1622a248df4f054f0ccf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838469"
---
# <a name="registering-and-enabling-an-iotimer-routine"></a>IoTimer ルーチンの登録と有効化





すべてのドライバーは、 [**Ioinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)を呼び出すことにより、1つまたは複数のデバイスオブジェクトを作成した後に、 [*iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンを登録できます。 ドライバーは、 [**Iostarttimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostarttimer)を呼び出すことによってタイマーを開始できます。 次の図は、これらの呼び出しを示しています。

![iotimer ルーチンの使用方法を示す図](images/3iotmer.png)

[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出してデバイスオブジェクトを作成すると、ドライバーは**ioinitializetimer**のエントリポイントと共に、ドライバーによって作成されたデバイスオブジェクトへのポインターと、ドライバーがあるコンテキスト領域を呼び出すことができます。*Iotimer*ルーチンが使用するすべてのコンテキストを保持します。 I/o マネージャーは、デバイスオブジェクトをカーネルに割り当てられたタイマーオブジェクトに関連付け、timer オブジェクトを毎秒タイムアウトに設定します。

ドライバーが**Iostarttimer**を呼び出した後、ドライバーが[**Iostarttimer er**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostoptimer)を呼び出すまで、 *iotimer*ルーチンは1秒間に1回呼び出されます。 ドライバーは、 **Iostarttimer**を使用して*iotimer*ルーチンへの呼び出しを再び有効にすることができます。 (多くの場合、ドライバーが**Iostarttimer**を呼び出すと、現在の IRP の i/o スタックの場所から取得したデバイスオブジェクトポインターが提供されます)。

エントリでは、 **Ioinitializetimer**を呼び出したときに、ドライバーが指定したコンテキストポインターと共に、 *iotimer*ルーチンにデバイス<em>オブジェクトポインターが</em>渡されます。

ドライバーは**Iost最適化 er**を*iotimer*ルーチン内から呼び出すことはできません。

I/o マネージャーは、指定されたデバイスオブジェクトのタイマールーチンの登録を解除し、ドライバーが[**Iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出すと、関連付けられているコンテキストを解放します。

 

 




