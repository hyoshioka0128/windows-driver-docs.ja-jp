---
title: バス マスター アダプター オブジェクトの割り当て
description: バス マスター アダプター オブジェクトの割り当て
ms.assetid: fc80d3f8-a12e-40bd-8b0e-c6bca2f9e7de
keywords:
- バス マスター アダプター オブジェクトの割り当てください。
- バス マスター DMA WDK カーネル
- DMA は、WDK カーネル、バス マスター DMA を転送します。
- アダプター オブジェクトの WDK カーネル、バス マスター DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1eb662a552dbf05ed25f25207a49d5b0062c28fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578913"
---
# <a name="allocating-the-bus-master-adapter-object"></a>バス マスター アダプター オブジェクトの割り当て





準備するパケットに基づく、バス マスターの DMA ドライバー呼び出し[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)と[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)後受信、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)または[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819). ドライバーは、これらのルーチンを呼び出し、前に、ディスパッチ ルーチンは IRP のパラメーターの有効性を確認する必要があります。 さらに処理するための別のドライバー ルーチンに IRP またキューにその可能性があります。 転送要求は、デバイスの I/O 操作を必要とする現在の IRP です。

ドライバーのルーチンを呼び出す**AllocateAdapterChannel** IRQL で実行する必要があります = ディスパッチ\_レベル。 によって返されるアダプター オブジェクトへのポインターと共に[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)を呼び出すときに、ドライバーは、次を指定する必要があります**AllocateAdapterChannel**:

-   現在の IRP の対象のデバイス オブジェクトへのポインター

-   エントリ ポイントの[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチン

-   コンテキストのドライバーにより決定された情報へのポインター、 *AdapterControl*ルーチンが使用されます

**AllocateAdapterChannel**キュー、ドライバーの*AdapterControl*アダプタ オブジェクトがないときに実行されるルーチンと一連の[レジスタにマップ](map-registers.md)ドライバーの dma が割り当てられましたターゲット デバイス間の操作です。

開始時、 *AdapterControl*ルーチンが指定された、*デバイス オブジェクト*と*コンテキスト*への呼び出しで渡されたポインター **AllocateAdapterChannel**、ハンドルと (*MapRegisterBase*) に割り当てられたマップに登録します。

*AdapterControl*ルーチンもへのポインターを指定は、**デバイス オブジェクト -&gt;CurrentIrp**ドライバーがある場合、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。 かどうか、ドライバー管理の Irp の専用キューではなく、 *StartIo* 、日常的なドライバー含める必要があります現在 IRP へのポインターを呼び出すときに渡すコンテキストの一部として**AllocateAdapterChannel**.

スキャッター/ギャザーの機能を使用しないバス マスター DMA デバイスのドライバー、 *AdapterControl*ルーチンは、次は、通常は。

1.  保存または DMA 操作に関するこのドライバーは、どのようなコンテキストを初期化します。 コンテキストは、入力を含めることがあります*MapRegisterBase*ハンドルを渡す必要があります、ドライバー [ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)と[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)、**長さ**I/O から要求された転送のバイト単位のスタック、IRP 内の場所などです。

2.  呼び出し[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)続けて**MapTransfer** (で説明されている[設定を転送操作](setting-up-a-transfer-operation.md)、[次へ]) を取得する、論理アドレス、デバイスは、転送操作の開始に使用できます。

3.  転送操作を開始するバス マスター アダプターを設定します。

4.  値を返します**DeallocateObjectKeepRegisters**します。

スキャッター/ギャザーの機能を備えたバス マスター デバイスのドライバーの*AdapterControl*ルーチンは、次は、通常は。

1.  保存、または初期化がどのような状態の保存などの DMA 操作について、ドライバーが保持、 *MapRegisterBase*ハンドルを渡す必要があります、ドライバー **MapTransfer**と**FlushAdapterBuffers**、**長さ**I/O から要求された転送のバイト単位のスタック、IRP 内の場所などです。

2.  呼び出し**MmGetMdlVirtualAddress**続けて**MapTransfer** (次のサブセクションで説明)、デバイスの論理アドレスを取得する転送操作の開始に使用できます。

    *AdapterControl*ルーチンを呼び出す MapTransfer 繰り返しまですべてバス マスター アダプターのスキャッター/ギャザーの一覧を作成、使用可能なマップを登録します。

3.  転送操作を開始するバス マスター アダプターを設定します。

4.  値を返します**DeallocateObjectKeepRegisters**します。

詳細については、次を参照してください。[書き込み AdapterControl ルーチン](writing-adaptercontrol-routines.md)します。

バス マスター DMA を実行するドライバーが使用することができます、 [ **GetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff546531)と[ **PutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff559967)ルーチン自分のデバイスをサポートするかどうかに関係なくスキャッター/ギャザー DMA します。 これらのルーチンを使用して、ドライバーの要件を変更*AdapterControl*ルーチン; を参照してください[を使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)詳細についてはします。

*AdapterControl*ルーチンは、IO の種類のシステム定義の値を返す必要があります\_割り当て\_アクション。 バス マスターの DMA を使用するドライバーに対して、 *AdapterControl*ルーチンでは、値を返す必要があります通常**DeallocateObjectKeepRegisters**、登録、ドライバーに割り当てられたマップを保持することができますターゲット デバイスは、現在の IRP のすべての要求されたデータを転送するまでをオブジェクト。 DPC ルーチンを呼び出す必要があります、転送が完了したら、 [ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)レジスタを割り当てられたマップを解放します。 場所、デバイスはサポートしていないコマンドは、次のキュー、ただしの場合、 *AdapterControl*ルーチンを返すことができます**KeepObject** IRP が現在の転送が完了すると DPC ルーチンを呼び出すことができます[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)代わりにします。

*AdapterControl*ルーチンは、DMA 操作を完了するバス マスター アダプターを待つことはできません。

バス マスター アダプターがスキャッター/ギャザーをサポートするかどうかに関係なく、 *AdapterControl*ルーチンでは、次を行う必要がありますには少なくとも。

1.  必要なコンテキスト情報を保存、特に、 *MapRegisterBase*処理: ドライバーのデバイスの拡張機能、コント ローラーの拡張機能、または他の常駐記憶域のドライバーにアクセス可能な領域 (非ページ プール、ドライバーによって割り当てられた)。 呼び出すときに、ドライバーはこのハンドルを渡す必要があります**MapTransfer**と**FlushAdapterBuffers**します。

2.  返す**DeallocateObjectKeepRegisters**します。

他のドライバー ルーチン (おそらく、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン) 呼び出す必要があります**FlushAdapterBuffers**各 DMA 転送操作が完了するとします。 このルーチンする必要があります設定も追加の DMA 操作を現在の IRP を満たすために必要です。

呼び出す必要がありますが、ドライバーは IRP が現在の転送要求を満たしていますか IRP が、デバイスまたはバス I/O エラーが原因で失敗する必要があります、 **FreeMapRegisters**します。 この呼び出しの最後の呼び出しの直後が発生する**FlushAdapterBuffers**の現在の IRP では、ドライバーは、バス上の他のデバイスの可能性があります、その他の DMA 要求を処理できるようにします。

 

 




