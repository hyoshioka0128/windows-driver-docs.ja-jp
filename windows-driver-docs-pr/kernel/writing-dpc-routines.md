---
title: 書き込み DPC ルーチン
description: 書き込み DPC ルーチン
ms.assetid: a0b93b71-7ee3-4626-b0b8-5dd6e19fba0d
keywords:
- 遅延プロシージャ呼び出しの WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65b662bd940d39ddb251bab5420ea76c48be4c3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560641"
---
# <a name="writing-dpc-routines"></a>書き込み DPC ルーチン





主な責務[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)と[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンは次のデバイスの I/O 操作があることが確認されますすぐに開始され、現在の IRP の完了します。

いずれかによって実行される追加の作業*DpcForIsr*または*CustomDpc*ルーチンは、ドライバーの設計と、デバイスの性質によって異なります。 たとえば、 *DpcForIsr*または*CustomDpc*ルーチンは行うことも、次のいずれか。

-   タイムアウトまたは失敗した操作を再試行してください。

-   呼び出す[ **IoAllocateErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff548245)を設定するレポート デバイス I/O エラー、および呼び出しのエラー ログ パケット[ **IoWriteErrorLogEntry**](https://msdn.microsoft.com/library/windows/hardware/ff550527)します。

    I/O エラーの処理の詳細については、[ログ エラー](logging-errors.md)を参照してください。

-   ドライバーで使用する場合[I/O バッファー](methods-for-accessing-data-buffers.md)、IRP では、デバイスの管理操作を指定する場合にシステムのバッファーに、デバイスから読み取ったデータの転送または**Irp -&gt;AssociatedIrp.SystemBuffer**IRP の完了前に

-   ドライバーで使用する場合[ダイレクト I/O](methods-for-accessing-data-buffers.md)とする必要がありますそれぞれ完了したばかりの部分的な転送操作の状態の保存の小さな部分に大規模な転送を中断は、次の部分的な転送範囲を計算し、ドライバーによって提供されるを使用して[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)次の部分的な転送操作のデバイスのプログラミング ルーチンです。

    バッファー内の I/O を使用しても、ドライバーは、そのデバイスには、転送機能が制限されている場合、転送要求を分割する必要があります。

-   ドライバーは、パケットに基づく DMA を使用している場合は、呼び出す[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)各転送操作のデバイス、および呼び出しの後に[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)または[ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)と一連の部分的な転送が行われ、完全転送要求が満たされています。

    要求された転送が 1 つの DMA 操作によって部分的にのみ満たされている場合、 *DpcForIsr*または*CustomDpc*ルーチンは、通常は IRP の指定したまでを設定する 1 つ以上の DMA 操作バイト数は、完全に転送されました。

    詳細については、DMA を使用して、[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)を参照してください。

-   ドライバー下手順 I/O (PIO) を使用する場合は、呼び出す[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) IRP が現在読み取りを要求する場合は、各転送操作の最後にします。

    要求された転送が、1 つの PIO 操作によって部分的にのみ満たされている場合、 *DpcForIsr*または*CustomDpc*ルーチンは、通常の IRP まで 1 つまたは複数の転送操作の設定指定したバイト数は、完全に転送されました。

    PIO の使用に関する詳細については、[を使用して直接 I/O](using-direct-i-o.md)を参照してください。

-   非 WDM ドライバーがある場合、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049) 、ルーチンの呼び出し[ **IoFreeController** ](https://msdn.microsoft.com/library/windows/hardware/ff549104)要求された操作が完了するとします。

なお、 *DpcForIsr*または*CustomDpc*ルーチンは、通常は、ドライバーのデバイスの I/O のほとんどを Irp を満たすために処理します。 これらのルーチンでは、ドライバーのディスパッチ ルーチンとデバイスにキューの Irp の責任の一部も共有します。

次を検討してください。 一般的な設計ガイドラインです。

-   任意*DpcForIsr*または*CustomDpc*ルーチンを呼び出す必要があります[**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358)この呼び出しに安全に行えるとすぐにつまり、なし。リソースの競合や競合状態をドライバーの使用可能性[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンまたはその他のルーチン、 *StartIo*ルーチンが原因で実行します。

-   ドライバーが、独自の Irp でキューを管理する場合、 *DpcForIsr*または*CustomDpc*は安全なは、[次へ] の IRP をキューから削除して、次の要求にデバイスを設定するとすぐに、ルーチンは、ドライバーを通知する必要があります。

A *DpcForIsr*または*CustomDpc*ルーチンを呼び出す必要があります**います**、それ以外の場合、適切なドライバー ルーチンを通知したりするときにデバイス I/O が、次の要求の処理起動できます。 によって、ドライバーとそのデバイスでは、これは、発生前にも、 *DpcForIsr*または*CustomDpc*ルーチンと現在の IRP の完了[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)、またはこのルーチンは、現在の IRP を完了し、コントロールを返します直前に発生することができます。

 

 




