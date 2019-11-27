---
title: デバイス拡張
description: デバイス拡張
ms.assetid: 9ea59994-1112-4ae5-96a8-fa0670694b53
keywords:
- デバイスオブジェクト WDK カーネル、デバイス拡張
- デバイス拡張機能 (WDK カーネル)
- 拡張機能-WDK デバイスオブジェクト
- 高レベルのドライバー拡張機能 (WDK カーネル)
- '下位レベルのドライバー拡張機能: WDK カーネル'
- 中間ドライバー拡張機能 (WDK カーネル)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac3c99868606fb658ac8f94e28024a8ab71f2e6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836943"
---
# <a name="device-extensions"></a>デバイス拡張





ほとんどの中間および最下位レベルのドライバーでは、デバイスの拡張機能は、デバイスオブジェクトに関連付けられている最も重要なデータ構造です。 内部構造はドライバーで定義され、通常は次のように使用されます。

-   デバイスの状態情報を保持します。

-   カーネル定義オブジェクトや、ドライバーで使用されるスピンロックなどの他のシステムリソースのストレージを提供します。

-   I/o 操作を実行するには、ドライバーが常駐し、システム領域に存在する必要があるデータを保持します。

ほとんどのバス、関数、およびフィルタードライバー (最下位レベルと中間ドライバー) は任意のスレッドコンテキストで実行されるため (最新の状態になっている任意のスレッドの場合)、デバイスの拡張機能は、デバイスの状態を維持するための各ドライバーのプライマリ場所です。ドライバーに必要なデバイス固有のデータ。 たとえば、 [*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンを実装するドライバーは、通常、デバイス拡張機能に必要なカーネル定義タイマーや dpc オブジェクトのストレージを提供します。

ISR を持つすべてのドライバーは、一連のカーネル定義の割り込みオブジェクトへのポインターの記憶域を提供する必要があり、ほとんどのデバイスドライバーは、デバイス拡張機能にこのポインターを格納します。 各ドライバーは、デバイスオブジェクトを作成するときにデバイス拡張機能のサイズを決定し、各ドライバーは独自のデバイス拡張機能の内容と構造を定義します。

I/o マネージャーの[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)と[**iocreateデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)のルーチンは、非ページメモリプールからデバイスオブジェクトと拡張機能にメモリを割り当てます。

IRP を受信するすべての標準ドライバールーチンも、要求された i/o 操作のターゲットデバイスを表すデバイスオブジェクトへのポインターを受け取ります。 これらのドライバールーチンは、このポインターを使用して、対応するデバイス拡張機能にアクセスできます。 通常、 *DeviceObject*ポインターは、下位レベルのドライバーの ISR に対する入力パラメーターでもあります。

次の図は、最下位レベルのドライバーのデバイスオブジェクトのデバイス拡張機能について、ドライバーで定義されたデータの代表的なセットを示しています。 上位レベルのドライバーは、 [**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)によって返され、KeSynchronizeExecution と[**io interrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)に渡さ[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)れる割り込みオブジェクトポインターのストレージを提供しません。 ただし、ドライバーに*Customtimerdpc*ルーチンがある場合は、次の図に示すように、高レベルのドライバーによってタイマーおよび dpc オブジェクトのストレージが提供されます。 上位レベルのドライバーでは、executive スピンロックおよびインタロックされたワークキュー用のストレージも提供される場合があります。

![最下位レベルのドライバーのデバイス拡張機能の例を示す図](images/3devext.png)

割り込みオブジェクトポインターのストレージを提供することに加えて、下位レベルのデバイスドライバーは、ISR が異なるベクター上の2つ以上のデバイスの割り込みを処理する場合、または複数の ISR がある場合に、割り込みスピンロックのストレージを提供する必要があります。 ISR の登録の詳細については、「 [isr の登録](registering-an-isr.md)」を参照してください。

通常、ドライバーは、図に示すように、デバイスの拡張機能にデバイスオブジェクトへのポインターを格納します。 ドライバーでは、デバイスのリソースリストのコピーを拡張機能に保存することもできます。

上位レベルのドライバーは、通常、次に下位にあるドライバーのデバイスオブジェクトへのポインターをそのデバイス拡張機能に格納します。 より高いレベルのドライバーは、次の下位にあるドライバーのデバイスオブジェクトへのポインターを[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)に渡す必要があります。これは、「 [irp の処理](handling-irps.md)」で説明されているように、irp で次の下位のドライバーの i/o スタック位置を設定した後に行います。

また、下位レベルのドライバーに対して Irp を割り当てる上位レベルのドライバーでは、新しい Irp で必要とされるスタック位置の数を指定する必要があることにも注意してください。 特に、上位レベルのドライバーが[**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)、 [**ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、または[**ioinitializer eirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)を呼び出す場合は、次の下位レベルのドライバーのターゲットデバイスオブジェクトにアクセスして、 **StackSize**の値を読み取る必要があります。これらのサポートルーチンの引数として、適切な*StackSize*を指定します。

上位レベルのドライバーは、 [**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)から返されたポインターを使用して、次の下位レベルのドライバーのデバイスオブジェクトからデータを読み取ることができますが、このようなドライバーは次の実装ガイドラインに従う必要があります。

-   下位のドライバーのデバイスオブジェクトにデータを書き込まないようにします。

    このガイドラインの唯一の例外として、ファイルシステムがあります。これは、低レベルのリムーバブルメディアドライバーのデバイスオブジェクトの**フラグ**で\_ボリュームを\_確認します。

-   次の理由により、下位のドライバーのデバイス拡張機能にアクセスしないようにしてください。

    -   2つのドライバー間で1つのデバイス拡張機能へのアクセスを同期する安全な方法はありません。
    -   このようなバックドア通信方式を実装するドライバーのペアは、個別にアップグレードすることはできません。また、既存のドライバーソースを変更せずに中間ドライバーを挿入することはできません。また、再コンパイルして、1つのウィンドウから簡単に移動することはできません。プラットフォームは次のようになります。

下位レベルのドライバーとの相互運用性を維持するために、1つの Windows プラットフォームまたはバージョンから次のように、上位レベルのドライバーは、指定された Irp を再利用するか、新しい Irp を作成する必要があります。また、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して要求をに渡す必要があります。下位レベルのドライバー。

 

 




