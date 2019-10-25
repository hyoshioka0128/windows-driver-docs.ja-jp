---
title: CustomDpc ルーチンの登録とキュー
description: CustomDpc ルーチンの登録とキュー
ms.assetid: 7c35f8f8-a6dc-43b1-9120-701227d7b4c5
keywords:
- CustomDpc
- CustomDpc ルーチンを登録しています
- CustomDpc ルーチンをキューに置いています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aeacfc3b2ae1c8fddcb53e7f31fa55ac56e87ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827514"
---
# <a name="registering-and-queuing-a-customdpc-routine"></a>CustomDpc ルーチンの登録とキュー





ドライバーは、デバイスオブジェクトを作成した後に[**Keinitializer Edpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)を呼び出すことによって、デバイスオブジェクトの[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンを登録します。 ドライバーは、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンからこの呼び出しを行うことができます。または、 [ **\_デバイス要求を開始\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を処理する[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)コードから呼び出すこともできます。

ドライバーの ISR が制御を返す直前に、 [**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)を呼び出して、 *customdpc*ルーチンの実行をキューにすることができます。 次の図は、これらのルーチンの呼び出しを示しています。

![customdpc ルーチンで dpc オブジェクトを使用する方法を示す図](images/3cstmdpc.png)

前の図に示すように、 *customdpc*ルーチンがあるドライバーは、dpc オブジェクトのストレージを提供する必要があります。 ドライバーは、ISR から DPC オブジェクトへのポインターを渡す必要があるため、記憶域は常駐システム領域メモリ内に存在する必要があります。 *Customdpc*ルーチンを使用したほとんどのドライバーは、デバイス拡張機能で DPC オブジェクトのストレージを提供しますが、ドライバーが[コントローラーオブジェクト](using-controller-objects.md)を使用している場合、またはドライバーによって割り当てられた非ページプールの場合は、記憶域をコントローラー拡張機能に含めることができます。

ドライバーが**Keinitializer Edpc**を呼び出す場合は、その*customdpc*ルーチンのエントリポイント、および DPC オブジェクト用のドライバーによって割り当てられたストレージへのポインターと、customdpc に渡されるドライバー定義のコンテキスト領域へのポインターを渡す必要があります。ルーチンが呼び出されたとき。 コンテキスト領域は IRQL = ディスパッチ\_レベルでアクセスできる必要があるため、常駐メモリ内に存在する必要もあります。

*DpcForIsr*ルーチンとは異なり、 *customdpc*ルーチンはデバイスオブジェクトに関連付けられていません。 ただし、通常、ドライバーには、 *Customdpc*ルーチンに渡されたコンテキスト情報内のターゲットデバイスオブジェクトと現在の IRP へのポインターが含まれます。 *DpcForIsr*ルーチンと同様に、 *customdpc*ルーチンはこの情報を使用して、ISR より低い IRQL で割り込みドリブン i/o 操作を完了します。

前の図に示すように、ISR は DPC オブジェクトへのポインター、およびドライバーで定義されている2つの追加のパラメーターを[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)に渡します。 コンピューターのすべてのプロセッサが、ディスパッチ\_レベル以上の IRQL で現在コードを実行している場合、DPC オブジェクトは、IRQL がプロセッサのディスパッチ\_レベルを下回るまでキューに置かれます。 次に、カーネルは DPC オブジェクトをデキューし、ドライバーの*Customdpc*ルーチンは、IRQL ディスパッチ\_レベルでプロセッサ上で実行されます。

任意の時点でキューに入れることができるのは、1つの DPC オブジェクトの1つのインスタンス化だけです。 したがって、ISR が同じ*Dpc*ポインターを使用して**KeInsertQueueDpc**を複数回呼び出す場合、ドライバーの*customdpc*ルーチンを実行する前に、IRQL がプロセッサのディスパッチ\_レベルを下回ると、 *customdpc*ルーチンが1回だけ実行されます。

*Customdpc*ルーチンは、割り込みの原因となった i/o 操作を完了するために必要な処理を行います。

ISR ルーチンと*Customdpc*ルーチンは、SMP コンピューターで同時に実行できます。 そのため、 *Customdpc*ルーチンを記述するときは、前のセクションで設定したガイドラインに従って、 [DpcForIsr ルーチンを登録してキューに登録](registering-and-queuing-a-dpcforisr-routine.md)します。

 

 




