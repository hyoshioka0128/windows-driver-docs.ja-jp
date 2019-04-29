---
title: CustomDpc ルーチンの登録とキュー
description: CustomDpc ルーチンの登録とキュー
ms.assetid: 7c35f8f8-a6dc-43b1-9120-701227d7b4c5
keywords:
- CustomDpc
- CustomDpc ルーチンを登録します。
- キューの CustomDpc ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8f265a45fd052996cc52fbe068b8e1b2490306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391104"
---
# <a name="registering-and-queuing-a-customdpc-routine"></a>CustomDpc ルーチンの登録とキュー





ドライバーの登録、 [ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)呼び出すことでデバイス オブジェクトの日常的な[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)デバイス作成後オブジェクト。 ドライバーからには、この呼び出しを行うことができます、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンまたは[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)を処理するコード[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。

呼び出すことができます、ドライバーの ISR に制御が戻る直前に[ **KeInsertQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552185)キューに、 *CustomDpc*ルーチンを実行します。 次の図は、これらのルーチンへの呼び出しを示しています。

![customdpc ルーチンの dpc オブジェクトを使用して説明する図](images/3cstmdpc.png)

前の図に示すように、ドライバーを持つ、 *CustomDpc*ルーチンは、DPC オブジェクトのストレージを提供する必要があります。 ドライバーは、ISR から DPC オブジェクトへのポインターを渡す必要があります、ために、記憶域は、常駐システム容量のメモリでなければなりません。 ほとんどのドライバーを*CustomDpc*ルーチンは、デバイスの拡張機能で、DPC オブジェクトに記憶域を提供するが、ストレージは、ドライバーで使用する場合、コント ローラーの拡張機能のことが、[コント ローラー オブジェクト](using-controller-objects.md)または非ページドライバーによって割り当てられたプール。

ドライバーを呼び出すと**KeInitializeDpc**エントリ ポイントを渡す必要がありますが、 *CustomDpc*とドライバーの定義のコンテキストに DPC オブジェクトのドライバーに割り当てられたストレージへのポインターとルーチン渡される領域で、 *CustomDpc*ルーチンが呼び出されるとします。 コンテキストの領域は、IRQL でアクセス可能である必要がありますので = ディスパッチ\_レベルにする必要がありますメモリ内に常駐します。

異なり、 *DpcForIsr*ルーチンを*CustomDpc*ルーチンは、デバイス オブジェクトに関連付けられていません。 ただし、ドライバーには、通常、ターゲット デバイスのオブジェクトへのポインターが含まれますに指定されたコンテキスト情報に現在の IRP、 *CustomDpc*ルーチン。 ように、 *DpcForIsr* 、ルーチン、 *CustomDpc*ルーチンでは、この情報を使用して、割り込み駆動 ISR よりも低い IRQL で I/O 操作を完了するには

前の図に示すように ISR がポインターを渡す DPC オブジェクトとに、ドライバーの定義は 2 つの追加のパラメーターに[ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)します。 コンピューターのすべてのプロセッサがディスパッチと同じかより大きい IRQL で実行中のコードを現在持って場合\_レベル、DPC は、オブジェクトのディスパッチの IRQL を下回るまではキューに配置\_プロセッサのレベル。 DPC オブジェクトと、ドライバーのカーネルが次に、デキュー *CustomDpc*ルーチンは IRQL のディスパッチに、プロセッサの実行\_レベル。

1 つの DPC オブジェクトの 1 つのインスタンスが作成は、特定の時点でキューに登録できます。 したがって ISR を呼び出す場合**KeInsertQueueDpc**同じ 2 回以上*Dpc*ドライバーの前にポインター *CustomDpc*ルーチンを実行すると、 *CustomDpc*ルーチンは IRQL を下回るディスパッチ後に 1 回だけ実行\_プロセッサのレベル。

A *CustomDpc*ルーチンは、割り込みの原因となった I/O 操作を完了するために必要なものが責任を負います。

ISR と*CustomDpc*ルーチンは、SMP マシン上で同時に実行することができます。 そのため、書き込み時に*CustomDpc*ルーチンでは、前のセクションでまとめられているガイドラインに従う[DpcForIsr ルーチンのキューの登録と](registering-and-queuing-a-dpcforisr-routine.md)します。

 

 




