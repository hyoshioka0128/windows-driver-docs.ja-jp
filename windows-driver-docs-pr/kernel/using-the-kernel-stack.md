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
ms.openlocfilehash: 714dce6251579ae4f1285fca3345ca7252c3bbf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372303"
---
# <a name="using-the-kernel-stack"></a>カーネル スタックの使用





カーネル モード スタックのサイズは、約 3 つのページに制限されます。 そのため、その内部のルーチンへのデータを渡すときに、ドライバーはカーネル スタックに大量のデータを渡すことはできません。

カーネル モード スタック領域不足を回避するには、次のデザイン ガイドラインを使用します。

-   各ルーチンは、カーネル スタックにデータを渡す場合、1 つのドライバーの内部ルーチンから深く入れ子になった呼び出しを行うしないでください。

-   ドライバーの再帰ルーチンを設計する場合に発生する可能性が再帰的な呼び出しの数を制限することを確認します。

つまり、ドライバーのコール ツリーの構造は比較的フラットになります。 呼び出すことができます、 [ **IoGetStackLimits** ](https://msdn.microsoft.com/library/windows/hardware/ff549299)と[ **IoGetRemainingStackSize** ](https://msdn.microsoft.com/library/windows/hardware/ff549286)カーネル スタックを判断するためのルーチンがされている領域使用可能なまたは[ **KeExpandKernelStackAndCallout** ](https://msdn.microsoft.com/library/windows/hardware/ff552030)を展開します。 カーネル モード スタックのサイズが異なるハードウェア プラットフォームや異なるバージョンのオペレーティング システムによって異なることができますに注意してください。

カーネル スタック領域不足では、致命的なシステム エラーが発生します。 ためのドライバーのことをお勧めそのため、[システム容量のメモリを割り当てる](allocating-system-space-memory.md)カーネル スタック領域不足を実行するよりもします。 ただし、非ページ プールも限られたシステム リソースです。

一般に、カーネル モード スタックは、場合によってはページ アウトできます、スレッドがユーザー モードを指定する待機状態になる場合がメモリに存在します。 参照してください[ **KeSetKernelStackSwapEnable** ](https://msdn.microsoft.com/library/windows/hardware/ff553262)カーネル スタックを現在のスレッドのページングを一時的に無効にする方法についてはします。 パフォーマンス上の理由がお勧めしませんカーネル スタックがグローバルにページングを無効にするには、デバッグ セッション中に実施する場合は、「[カーネル スタックのページングを無効にします。](https://msdn.microsoft.com/library/windows/hardware/ff541920)

カーネル スタックにページ アウトできる場合があります、ため、DMA または DISPATCH_LEVEL 以上を実行している任意のルーチンにスタック ベースのバッファー (つまりローカル変数) を渡すことに注意してください。

