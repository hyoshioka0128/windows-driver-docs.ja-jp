---
title: DMA のパケット ベースのシステムの DMA コント ローラーの設定
description: DMA のパケット ベースのシステムの DMA コント ローラーの設定
ms.assetid: 3a646169-1ea3-4844-b771-d08f4ddec460
keywords:
- DMA WDK カーネルでは、パケットに基づくシステム
- DMA WDK カーネルのパケットに基づく
- DMA は、パケットに基づく、WDK のカーネルを転送します。
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f713a72bda7b8fa3be399233e14f6de9bed80b61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529204"
---
# <a name="setting-up-the-system-dma-controller-for-packet-based-dma"></a>DMA のパケット ベースのシステムの DMA コント ローラーの設定





ときに[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)にドライバーの制御を転送[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504) 、日常的なドライバー「所有」DMA システムコント ローラーと一連のレジスタにマップします。 次に、ドライバーは、次の図に示すように、転送操作では、DMA コント ローラーを設定する必要があります。

![プログラミング システムの dma コント ローラーを示す図](images/3dmaptsf.png)

ドライバーがある場合、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン、 [ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)へのポインターを渡す**デバイス オブジェクト&gt;CurrentIrp**で、 *PIrp*パラメーターを*AdapterControl*ルーチン。 渡すコンテキストの一部としてドライバーが IRP が現在へのポインターを含める必要がある場合、ただし、ドライバーは Irp のキューを管理、 *AdapterControl*します。

前図に示すよう、ドライバーの*AdapterControl*ルーチンは次のように、DMA 転送を設定します。

1.  *AdapterControl*ルーチンは、転送を開始する位置のアドレスを取得します。 IRP を満たすために必要な初期転送の*AdapterControl*ルーチンの呼び出し[ **MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539)、ポインターで MDL を渡して**Irp -&gt;MdlAddress**、この DMA 転送、バッファーを記述します。

    **MmGetMdlVirtualAddress**ドライバーとして使用できるインデックス システムの物理アドレスの転送を開始位置となる仮想アドレスを返します。

    IRP では、1 つ以上の転送操作が必要とする場合、ドライバーは、このセクションで後述するよう更新された開始アドレスを計算します。

2.  *AdapterControl*ルーチンによって返されるアドレスを保存します**MmGetMdlVirtualAddress**または手順 1. で計算します。 このアドレスは必須パラメーター (*CurrentVa*) に[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)します。

3.  *AdapterControl*ルーチンの呼び出し**MapTransfer**次のパラメーターを指定して、システム DMA コント ローラーを設定します。

    -   によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

    -   ポインター (*Mdl*) で MDL に**Irp -&gt;MdlAddress**現在 IRP の

    -   *MapRegisterBase*にドライバーのハンドルが渡される*AdapterControl*で日常的な**AllocateAdapterChannel**

    -   値 (*CurrentVa*) によって返される**MmGetMdlVirtualAddress**場合、最初の呼び出しは**MapTransfer** IRP の

        それ以外の場合、ドライバーを提供、更新された*CurrentVa*バッファーの次の転送で操作を開始位置を示す値。

    -   変数へのポインター (*長さ*) この転送バイト数を示す

        ドライバーが 1 回の呼び出しですべての要求されたデータを転送かどうか**MapTransfer** 、DMA 操作でデバイス固有の制約がないと*長さ*の値に設定することができます**長さ**ドライバーの I/O の IRP の場所をスタックします。 長さ (バイト単位) は、最大で (ページ\_サイズ\*、 *NumberOfMapRegisters*によって返される[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220))。 説明したように、要求に分割する必要があります、ドライバーのそれ以外の場合、[転送要求の分割](splitting-dma-transfer-requests.md)の値を更新する必要がありますと*長さ*に後続の呼び出しで**MapTransfer**現在 IRP の。

    -   ブール値 (*WriteToDevice*)、(システム メモリからデータをデバイスに転送) は true、転送操作の方向を示す

    **MapTransfer**論理アドレスを返します。 システム DMA を使用するドライバーには、この値を無視する必要があります。

4.  *AdapterControl*ルーチンは、DMA 操作については、デバイスを設定します。

5.  *AdapterControl*ルーチンを返します。 **KeepObject**します。

デバイスでは、その現在の DMA 操作が完了したことを示します、ドライバーで呼び出す必要があります[ **FlushAdapterBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff545917)、通常は、ドライバーから[ *DpcForIsr*](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン。

*DpcForIsr*ルーチンまたは DMA 操作を完了する別のドライバーのルーチンを呼び出す**FlushAdapterBuffers** DMA システムにキャッシュされているすべてのデータを確実に、コント ローラーがシステム メモリに読み込まれるか、書き込むデバイスです。 同じルーチンも呼び出す必要があります**MapTransfer**もう一度現在 IRP のより多くのデータを転送するシステムの DMA コント ローラーを再設定する必要がある場合。 同様に、呼び出す必要があります**FlushAdapterBuffers**各転送操作をもう一度次です。

場合は、ドライバーを呼び出す必要があります**MapTransfer**同じアダプター オブジェクトのポインターを提供、現在の IRP の 2 回以上*Mdl*ポインター、 *MapRegisterBase*を処理し、すべての呼び出しの方向を転送します。 ただし、ドライバーを更新する必要があります、 *CurrentVa*と*長さ*パラメーターを 2 つ目と、後続の呼び出し前に**MapTransfer**します。 これらの各パラメーターの更新後の値を計算するには、次の数式を使用します。

-   *CurrentVa* = *CurrentVa* + (*長さ*前の呼び出しで要求された**MapTransfer**)

-   *長さ*= 最小 (残り**長さ**転送する (ページ\_サイズ\* *NumberOfMapRegisters*によって返される**IoGetDmaAdapter**))

その DMA の転送に関するコンテキスト情報各ドライバーを維持する必要がありますは、その特定のデバイスのニーズによって異なります。 一般的なコンテキストが MDL に現在の仮想アドレスを含めることがあります (*CurrentVa*)、これまでに転送する可能性がある現在の IRP では、その他の情報へのポインターに残りのバイト数に転送されるバイト数、ドライバー開発者を対象と便利です。

要求された転送が完了すると、またはドライバーを呼び出す必要がある場合は、ドライバーは IRP のエラー状態を返す必要があります、 [ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)他のシステムの DMA コント ローラーを解放するには、すぐにドライバーは、このドライバーを使用します。

 

 




