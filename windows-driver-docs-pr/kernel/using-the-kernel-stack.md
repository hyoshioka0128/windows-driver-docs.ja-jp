---
title: カーネル スタックの使用
description: カーネル スタックの使用
ms.assetid: f1df01f4-f156-4267-a4a0-c548e16c02ea
keywords:
- メモリ管理の WDK カーネル、カーネル スタック
- カーネル モード スタック領域 WDK
- カーネル スタック領域 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e57d924daff5ca1de975af0b5afb4daa04076b80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358187"
---
# <a name="using-the-kernel-stack"></a>カーネル スタックの使用





カーネル モード スタックのサイズは、約 3 つのページに制限されます。 そのため、その内部のルーチンへのデータを渡すときに、ドライバーはカーネル スタックに大量のデータを渡すことはできません。

カーネル モード スタック領域不足を回避するには、次のデザイン ガイドラインを使用します。

-   各ルーチンは、カーネル スタックにデータを渡す場合、1 つのドライバーの内部ルーチンから深く入れ子になった呼び出しを行うしないでください。

-   ドライバーの再帰ルーチンを設計する場合に発生する可能性が再帰的な呼び出しの数を制限することを確認します。

つまり、ドライバーのコール ツリーの構造は比較的フラットになります。 呼び出すことができます、 [ **IoGetStackLimits** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetstacklimits)と[ **IoGetRemainingStackSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetremainingstacksize)カーネル スタックを判断するためのルーチンがされている領域使用可能なまたは[ **KeExpandKernelStackAndCallout** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keexpandkernelstackandcallout)を展開します。 カーネル モード スタックのサイズが異なるハードウェア プラットフォームや異なるバージョンのオペレーティング システムによって異なることができますに注意してください。

カーネル スタック領域不足では、致命的なシステム エラーが発生します。 ためのドライバーのことをお勧めそのため、[システム容量のメモリを割り当てる](allocating-system-space-memory.md)カーネル スタック領域不足を実行するよりもします。 ただし、非ページ プールも限られたシステム リソースです。

一般に、カーネル モード スタックは、場合によってはページ アウトできます、スレッドがユーザー モードを指定する待機状態になる場合がメモリに存在します。 参照してください[ **KeSetKernelStackSwapEnable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kesetkernelstackswapenable)カーネル スタックを現在のスレッドのページングを一時的に無効にする方法についてはします。 パフォーマンス上の理由がお勧めしませんカーネル スタックがグローバルにページングを無効にするには、デバッグ セッション中に実施する場合は、「[カーネル スタックのページングを無効にします。](https://docs.microsoft.com/windows-hardware/drivers/debugger/disable-paging-of-kernel-stacks)

カーネル スタックにページ アウトできる場合があります、ため、DMA または DISPATCH_LEVEL 以上を実行している任意のルーチンにスタック ベースのバッファー (つまりローカル変数) を渡すことに注意してください。

