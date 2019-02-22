---
title: 一般的なバッファー システム DMA 用アダプター、チャネルの割り当てください。
description: 一般的なバッファー システム DMA 用アダプター、チャネルの割り当てください。
ms.assetid: 3b426b5e-e555-458c-8e16-0d59a7cb9bd6
keywords:
- アダプタのチャネルの割り当てください。
- アダプター チャネル割り当て WDK カーネル
- AllocateAdapterChannel
- システム DMA WDK カーネルでは、一般的なバッファー
- 一般的なバッファー DMA WDK カーネル
- DMA は、WDK カーネルでは、一般的なバッファーを転送します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5efb04bf7a49f1c2b10e02069f860222b491bd43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532771"
---
# <a name="allocating-an-adapter-channel-for-common-buffer-system-dma"></a>一般的なバッファー システム DMA 用アダプター、チャネルの割り当てください。





ドライバーを呼び出す[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)後その[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン (または DMA の転送を処理するその他の任意のディスパッチ ルーチン) に IRP のパラメーターの有効性をチェック、場合によってさらに処理する、別のドライバーのルーチンを 1 つまたは複数の Irp キューに登録され読み込まれる可能性があります、該当する場合は、転送されるデータと共通のバッファー。

ドライバーのルーチンを呼び出す**AllocateAdapterChannel** IRQL で実行する必要があります = ディスパッチ\_レベル。 **AllocateAdapterChannel**ルーチンのキュー、ドライバーの[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチンで、システムの DMA コント ローラーがこのドライバーに割り当てられた後に実行し、設定の[レジスタにマップ](map-registers.md)がドライバーの DMA 操作に割り当てられました。

エントリの*AdapterControl*ルーチンをデバイス オブジェクトと呼び出しで渡されるコンテキスト ポインターが与えられます**AllocateAdapterChannel**とともに、割り当てられたマップへのハンドルとして登録します。 *AdapterControl*ルーチンもへのポインターを指定は、**デバイス オブジェクト -&gt;CurrentIrp**ドライバーがある場合、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。 かどうか、ドライバー管理の Irp の専用キューではなく、 *StartIo* 、日常的なドライバー含める必要があります現在 IRP へのポインターを呼び出すときに渡すコンテキスト データの一部として**AllocateAdapterChannel**.

*AdapterControl*ルーチンは、次を通常は。

1.  保存または DMA 操作に関するこのドライバーは、どのようなコンテキストを初期化します。 コンテキストは、入力を含めることがあります*MapRegisterBase*ハンドルを渡す必要があります、ドライバー [ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)と[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)と、おそらく、**長さ**I/O から要求された転送の IRP 内の場所をスタックします。

2.  転送操作を開始する下位のデバイスを設定します。

3.  値を返します**KeepObject**します。

詳細については、次を参照してください。[書き込み AdapterControl ルーチン](writing-adaptercontrol-routines.md)します。

システム DMA コント ローラーの自動初期化モードを使用するドライバーに対して、 *AdapterControl*ルーチンは、値を返す必要があります**KeepObject**します。 これにより、システムの DMA コント ローラーの「所有者」を保持するドライバーとマップ register(s) を割り当てられているすべてのデータを転送するまでです。

*AdapterControl*ルーチンは、DMA 操作を実行する下位のデバイスを待つことができない、 *AdapterControl*ルーチンでは、次を行う必要がありますには少なくとも。

1.  コンテキスト情報を保存、特に*MapRegisterBase*ドライバーのデバイスの拡張機能、コント ローラーの拡張機能、またはその他のドライバーにアクセス可能な常駐ストレージ領域に (ドライバーによって割り当てられた非ページ プール) のハンドル。

2.  返す**KeepObject**します。

他のドライバー ルーチン (おそらく、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン) 呼び出す必要があります[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)と[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507) DMA 転送操作が完了するとします。

 

 




