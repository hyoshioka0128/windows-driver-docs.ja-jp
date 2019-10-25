---
title: 使用する必要がある DPC の種類
description: 使用する必要がある DPC の種類
ms.assetid: 7a8e6d75-5573-4a94-a895-fa2f70856807
keywords:
- 遅延プロシージャ呼び出し WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e8178244e1f939b6a9a40aaecb5afa571b39d3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838315"
---
# <a name="which-type-of-dpc-should-you-use"></a>使用すべき DPC の種類





ドライバーの設計によっては、次のいずれかを使用できます。

-   すべての割り込みドリブン i/o 操作を完了するための単一の[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)

-   1つ以上の[*Customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンのセット。

-   *DpcForIsr*と一連の操作固有の*customdpc*ルーチン

ドライバーに1つの*DpcForIsr*ルーチン、一連の*customdpc*ルーチン、またはその両方が含まれているかどうかは、基になるデバイスの性質と、それがサポートする必要がある i/o 要求のセットによって異なります。

最も下位レベルのデバイスドライバーには、それぞれのデバイスで1つ以上の操作を必要とする各 IRP の i/o 処理を完了するための*DpcForIsr*ルーチンが1つあります。 1つの*DpcForIsr*を使用して、一度に1つの操作を実行するデバイス上で、要求ごとの割り込みドリブン i/o 操作を完了することは比較的簡単です。 このようなドライバーの ISR では、割り込みドリブン i/o 操作ごとに[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出す必要があります。

いくつかの下位レベルのドライバーでは、デバイスで割り込みドリブン i/o 操作のさまざまなセットを完了するために複数の DPC が必要でない限り、 *Customdpc*ルーチンがあります。

1つの*DpcForIsr*を使用して、同時操作を行うことができるデバイスでの割り込みドリブン i/o 操作を完了するには、慎重に設計する必要がありますが、比較的困難になることがあります。 ISR では、 *DpcForIsr*をキューに追加するだけでなく、 [**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)を呼び出すことによって、ドライバーが提供する一連の*customdpc*ルーチンをキューに追加できます。

たとえば、シリアルドライバーの作成に関係する設計上の課題の一部を考えてみましょう。 全二重デバイスのドライバーとして、シリアルドライバーは、Irp が*StartIo*ルーチンにキューに置かれている順序と、マルチタスキングのマルチプロセッサシステムでデバイスからの割り込みのシーケンスとの間に1対1で対応することはできません。 さらに、シリアルドライバーは、前に要求された操作をキャンセルしたり、バッファー内のデータを消去したりするために、タイムアウト要求と非同期のユーザー生成要求を処理する必要があります。

その結果、シリアルドライバーは、ユーザーモードの COM ポートアプリケーションが要求できる読み取り、書き込み、消去、待機の各操作に対して内部キューを維持する場合があります。 また、参照カウントを維持したり、内部キュー内の Irp に対して、一連のフラグなどの他の追跡メカニズムを使用したりすることもできます。 その ISR は、ドライバーによって提供される*customdpc*ルーチンに関連付けられている、さまざまなドライバー割り当ておよび初期化済み dpc オブジェクトを使用して**KeInsertQueueDpc**を呼び出します。

 

 




