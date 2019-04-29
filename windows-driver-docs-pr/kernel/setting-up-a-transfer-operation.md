---
title: 転送操作のセットアップ
description: 転送操作のセットアップ
ms.assetid: cabac16d-b946-4b96-af2c-5fd0a0d848da
keywords:
- バス マスター DMA WDK カーネル
- DMA は、WDK カーネル、バス マスター DMA を転送します。
- アダプター オブジェクトの WDK カーネル、バス マスター DMA
- 論理アドレスの範囲を WDK DMA
- WDK DMA のアドレス
- 転送操作 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbeb0007d2c637a21dd0968f9d4c8c880fb86e96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385528"
---
# <a name="setting-up-a-transfer-operation"></a>転送操作のセットアップ





ときに[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)にドライバーの制御を転送[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504) 、日常的な割り当て済みのマップ セット登録します。 ただし、ドライバーする必要があります現在 IRP の譲渡要求の物理メモリをシステムようにマップ、バス マスター アダプターの論理アドレスの範囲。

1.  呼び出す[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)で MDL で**Irp -&gt;MdlAddress**転送が開始する必要があります、システムの物理アドレスのインデックスを取得します。

    戻り値が必要なパラメーター (*CurrentVa*) に[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)します。

2.  呼び出す**MapTransfer** IRP のバッファーのシステムの物理アドレスの範囲をバス マスター アダプターの論理アドレスの範囲にマップします。

ドライバーは、転送操作のアダプターを設定できます。 次の図では、転送を設定する手順を示します。

![転送操作の設定を示す図します。](images/3dmabus.png)

前図に示すよう、ドライバーの*AdapterControl*ルーチンは次のようにバス マスターの DMA 操作を設定します。

1.  *AdapterControl*ルーチンは、転送を開始する位置のアドレスを取得します。 IRP を満たすために必要な初期転送の*AdapterControl*ルーチンの呼び出し[ **MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539)、ポインターで MDL を渡して**Irp -&gt;MdlAddress**、この DMA 転送、バッファーを記述します。

    **MmGetMdlVirtualAddress**ドライバーとして使用できるインデックス システムの物理アドレスの転送を開始位置となる仮想アドレスを返します。

    IRP では、1 つ以上の転送操作が必要とする場合、ドライバーは、このセクションで後述するよう更新された開始アドレスを計算します。

2.  *AdapterControl*ルーチンによって返されるアドレスを保存します**MmGetMdlVirtualAddress**または手順 1. で計算します。 このアドレスは必須パラメーター (*CurrentVa*) に[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)します。

3.  *AdapterControl*ルーチンの呼び出し**MapTransfer**、位置、ドライバーが転送操作を開始するバス マスター アダプターをプログラミングできる論理アドレスが返されます。 呼び出しで**MapTransfer**ドライバーは、次のパラメーターを提供します。
    -   によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

    -   MDL へのポインター **Irp -&gt;MdlAddress**現在 IRP の

    -   *MapRegisterBase*にドライバーのハンドルが渡される*AdapterControl*で日常的な**AllocateAdapterChannel** (を参照してください[バス マスターの割り当てアダプター オブジェクト](allocating-the-bus-master-adapter-object.md))

    -   によって返される値**MmGetMdlVirtualAddress**場合、最初の呼び出しは**MapTransfer**現在 IRP の

        それ以外の場合、ドライバーを提供、更新された*CurrentVa*実行する次の物理-論理マッピングを示す値。 (更新済みの計算方法*CurrentVa*は後でこのセクションで説明します)。

    -   変数へのポインター (*長さ*)、この転送バイト数を示します

        ドライバーが十分なマップのレジスタを単一の DMA 操作で要求されたすべてのデータを転送するが、その DMA 操作でデバイス固有の制約がない場合、*長さ*の値に設定することができます**長さ**ドライバーの I/O の IRP の場所をスタックします。 入力文字列の長さ (バイト単位) は、最大で (ページ\_サイズ\*、 *NumberOfMapRegisters*によって返される**IoGetDmaAdapter**)。 説明したように、要求に分割する必要があります、ドライバーのそれ以外の場合、[転送要求の分割](splitting-dma-transfer-requests.md)の値を更新する必要がありますと*長さ*に後続の呼び出しで**MapTransfer**現在 IRP の。

    -   ブール値 (*WriteToDevice*)、(デバイスにメモリからのデータを転送) は true、転送操作の方向を示す

4.  *AdapterControl*ルーチンは、DMA 操作については、デバイスを設定します。

5.  *AdapterControl*ルーチンを返します。 **DeallocateObjectKeepRegisters**します。

場合は、ドライバーを呼び出す必要があります**MapTransfer**同じアダプター オブジェクトのポインターを提供する現在の IRP を満たすために 2 回以上*Mdl*ポインター、 *MapRegisterBase*を処理します。呼び出すたびに方向を転送および**MapTransfer**します。 ただし、ドライバーを提供する必要があります更新*CurrentVa*と*長さ*を 2 回目以降の呼び出しで値**MapTransfer**します。 これらの値を計算するのにには、次の数式を使用します。

-   *CurrentVa* = *CurrentVa* + (*長さ*への呼び出しの前で要求された**MapTransfer**)

-   *長さ*= 最小 (残り**長さ**転送する (ページ\_サイズ\* *NumberOfMapRegisters*によって返される**IoGetDmaAdapter**))

その DMA の転送に関するコンテキスト情報各ドライバーを維持する必要がありますは、その特定のデバイスのニーズによって異なります。 一般的なコンテキストが MDL に現在の仮想アドレスを含めることがあります (*CurrentVa*)、ここまでは、転送、および場合によっては、現在の IRP へのポインターに残りのバイト数に転送されたバイト数。

スキャッター/ギャザー機能により、デバイスのドライバー、*長さ*パラメーターを**MapTransfer**入力と出力の両方のパラメーターです。 戻り時にから**MapTransfer**システムがマップされているデータのバイト数を示します。 戻り値である、*長さ*、返された論理アドレスと組み合わせて、バス マスター アダプターがこの DMA 操作で転送のこの部分を使用できる論理アドレスの範囲を示します。

**注**  ため*長さ*によって上書き**MapTransfer**、この実装のガイドラインに従ってください。ポインターを渡すことはありません、**長さ**ドライバーの I/O スタックとして IRP の場所、*長さ*パラメーターを**MapTransfer**デバイスは、スキャッター/ギャザーをサポートしている場合。

これを行うと、現在 IRP がドライバーが要求されたすべてのデータを転送するかどうかを判断することは不可能で値が破棄でした。

 

DMA 操作ごとの最後に、ドライバーを呼び出す必要があります[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)有効なアダプター オブジェクト ポインターを使用して、 *MapRegisterBase*ことを確認しますすべてへのハンドル、データが転送された現在の DMA 操作の物理-論理マッピングを解放するとします。 呼び出す必要がありますが、ドライバーは、現在 IRP を満たすために追加の DMA 操作を設定する必要がある場合、 **FlushAdapterBuffers**各転送操作の完了後します。

要求されたすべての転送が完了するか、ドライバーは IRP のエラー状態を返す必要があります、ときに、ドライバーを呼び出す必要があります[ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)その最後の呼び出しの直後に**FlushAdapterBuffers**バス マスター アダプターの最適なスループットを取得するためにします。 呼び出しで**FreeMapRegisters**、ドライバーは、前の呼び出しに渡されるアダプター オブジェクトのポインターを渡す必要があります**AllocateAdapterChannel**します。

 

 




