---
title: デバイス拡張
description: デバイス拡張
ms.assetid: 9ea59994-1112-4ae5-96a8-fa0670694b53
keywords:
- デバイス オブジェクトの WDK カーネル、デバイスの拡張機能
- デバイスの拡張機能の WDK カーネル
- WDK のデバイス オブジェクトの拡張機能
- 高度なドライバーの拡張機能の WDK カーネル
- 下位レベルのドライバー拡張機能の WDK カーネル
- 中間ドライバー拡張機能の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230f5c3e2f96d3ef8ed0a5fd236a92fa365a0fe7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385015"
---
# <a name="device-extensions"></a>デバイス拡張





ほとんどの中間的な最下位レベルのドライバーは、デバイス拡張機能は、デバイス オブジェクトに関連付けられている最も重要なデータ構造です。 その内部構造は、ドライバーの定義し、は、通常を使用します。

-   デバイスの状態情報を維持します。

-   カーネル定義オブジェクトまたは、ドライバーによって使用される、スピン ロックなどの他のシステム リソースのストレージを提供します。

-   常駐しており、その I/O 操作を実行するシステムの領域で、ドライバーのデータがありますを保持します。

実行されるため、ほとんどのバス、関数、およびフィルター ドライバー (最下位レベルおよび中間ドライバー) (ことのどのスレッドがある現在) 任意のスレッド コンテキストでは、デバイスの拡張機能は、状態、および他のすべてのデバイスを維持するために各ドライバーのプライマリの場所デバイスに固有のデータ、ドライバーが必要です。 たとえば、実装するドライバー、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチンは通常、必要なのストレージを提供タイマーのカーネル定義やデバイスの拡張機能で DPC オブジェクト。

ISR のあるすべてのドライバーは、一連の割り込みのカーネル定義のオブジェクトへのポインターの記憶域を提供する必要があり、ほとんどのデバイス ドライバーは、デバイスの拡張機能でこのポインターを格納します。 各ドライバーは、デバイス オブジェクトを作成し、各ドライバーは、内容と、独自のデバイスの拡張機能の構造を定義するときに、デバイスの拡張機能のサイズを決定します。

I/O マネージャーの[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)と[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)ルーチンでは、デバイス オブジェクトと拡張機能のメモリを割り当てる非ページ メモリ プール。

IRP を受信するすべての標準のドライバー ルーチンでは、要求された I/O 操作のターゲット デバイスを表すデバイス オブジェクトへのポインターも受信します。 これらのドライバーのルーチンは、このポインターを通じて、対応するデバイスの拡張機能にアクセスできます。 通常、*デバイス オブジェクト*ポインターは、最下位レベルのドライバーの ISR. への入力パラメーターでも

次の図は、デバイスの拡張機能のデバイス オブジェクトの最下位レベル ドライバーのドライバーの定義済みのデータの代表的なセットを示します。 高度なドライバーがによって返される割り込みオブジェクト ポインターの記憶域を提供しない[ **IoConnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)に渡されると[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)と[ **IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)します。 ただしより高度なドライバーはタイマーと、ドライバーがある場合は、次の図に示す DPC オブジェクト ストレージを提供する*CustomTimerDpc*ルーチン。 高度なドライバーはまた executive スピンロックの記憶域を提供する可能性があり、作業キューをインター ロックします。

![最下位レベルのドライバーの拡張機能をデバイスの使用例を示す図](images/3devext.png)

割り込みオブジェクト ポインターのストレージを提供するだけでなく、最下位レベルのデバイス ドライバーが必要割り込みスピン ロックの記憶域その ISR がさまざまなベクトルまたは 1 つ以上の ISR. があるかどうかに 2 つまたは複数のデバイスの割り込みを処理する場合 ISR の登録の詳細については、次を参照してください。[登録 ISR](registering-an-isr.md)します。

通常、ドライバーは、図に示すように、そのデバイスの拡張機能で、デバイス オブジェクトへのポインターを格納します。 ドライバーは、拡張機能にデバイスのリソースの一覧のコピーを保持も可能性があります。

高度なドライバーは通常、そのデバイスの拡張機能で、次の下位ドライバーのデバイス オブジェクトへのポインターを格納します。 高度なドライバーが、次の下位ドライバーのデバイス オブジェクトへのポインターを渡す必要があります[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)で説明したように、IRPで、次の下位ドライバーのI/Oスタックの場所の設定が後に、[Irp の処理](handling-irps.md)します。

また、Irp を下位レベルのドライバーによって割り当てられる任意の高度なドライバーが新しい Irp が必要数のスタックの場所を指定する必要があります。 特により高度なドライバーを呼び出す場合[ **IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iomakeassociatedirp)、 [ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)、または[ **IoInitializeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeirp)、読み取る次下位ドライバーの対象のデバイス オブジェクトにアクセスする必要があります、 **StackSize** 、適切なを指定するには、値*StackSize*これらへの引数としてルーチンをサポートします。

によって返されるポインターを通じて、次の下位レベルのドライバーのデバイス オブジェクトより高度なドライバーがデータの読み取り中に[ **IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)、このようなドライバーがこれらに従う必要があります実装のガイドライン:

-   下位のドライバーのデバイス オブジェクトにデータを書き込みを試みることはありません。

    このガイドラインに対する唯一の例外が設定され、オフにするファイル システム\_を確認してください\_内のボリューム、**フラグ**の下位レベルのリムーバブル メディアのドライバーのデバイス オブジェクト。

-   次の理由で下位のドライバーのデバイスの拡張機能へのアクセスを試行しない:

    -   2 つのドライバーの間、1 つのデバイスの拡張機能へのアクセスを同期する安全な方法はありません。
    -   バックドアの通信のスキームを実装しているドライバーのペアを個別にアップグレードすることはできません、既存のドライバー ソースを変更することがなくそれらの間に挿入された中間のドライバーを含めることはできませんできません再コンパイルおよび 1 つの Windows から簡単に移動次のプラットフォームです。

次から 1 つの Windows プラットフォームまたはバージョンより低いレベル ドライバーとの相互運用性を維持するより高度なドライバーいずれかに許可する Irp を再利用する必要がありますまたは新しい Irp を作成する必要があり、それらを使用する必要があります[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)下位レベルのドライバーに要求を伝達します。

 

 




