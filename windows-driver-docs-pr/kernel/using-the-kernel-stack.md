---
title: カーネルスタックの使用
description: カーネルスタックの使用
ms.assetid: f1df01f4-f156-4267-a4a0-c548e16c02ea
keywords:
- メモリ管理 (WDK カーネル、カーネルスタック)
- カーネルモードのスタック領域 WDK
- カーネルスタック領域 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd0a7bc828bb1b0044f71bf476e25343482dde7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838329"
---
# <a name="using-the-kernel-stack"></a>カーネルスタックの使用





カーネルモードスタックのサイズは、約3ページに制限されています。 したがって、データを内部ルーチンに渡す場合、ドライバーはカーネルスタックで大量のデータを渡すことはできません。

カーネルモードのスタック領域が不足しないようにするには、次の設計ガイドラインに従います。

-   各ルーチンがカーネルスタックにデータを渡す場合は、内部ドライバールーチンから別の内部ドライバールーチンに深く入れ子になった呼び出しを行わないようにします。

-   再帰ルーチンを含むドライバーを設計する場合は、発生する可能性がある再帰呼び出しの回数を制限してください。

つまり、ドライバーのコールツリー構造は比較的フラットである必要があります。 [**Iogetstacklimits**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetstacklimits)と[**IoGetRemainingStackSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetremainingstacksize)ルーチンを呼び出して、使用可能なカーネルスタック領域を特定したり、 [**Keexpandkernel stackand吹き出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keexpandkernelstackandcallout)を呼び出して拡張したりすることができます。 カーネルモードスタックのサイズは、ハードウェアプラットフォームとオペレーティングシステムのバージョンによって異なる場合があることに注意してください。

カーネルスタック領域が不足すると、致命的なシステムエラーが発生します。 そのため、カーネルスタック領域が不足しているよりも、ドライバーが[システム領域メモリを割り当てる](allocating-system-space-memory.md)方が適切です。 ただし、非ページプールもシステムリソースに制限されています。

通常、カーネルモードスタックはメモリに存在しますが、スレッドがユーザーモードを指定する待機状態になると、ページングされることがあります。 現在のスレッドのカーネルスタックページングを一時的に無効にする方法については、「 [**Kesetkernel Stackswapenable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kesetkernelstackswapenable) 」を参照してください。 パフォーマンス上の理由から、カーネルスタックのページングをグローバルに無効にすることは推奨されていませんが、デバッグセッション中に実行する場合は、「[カーネルスタックのページングを無効](https://docs.microsoft.com/windows-hardware/drivers/debugger/disable-paging-of-kernel-stacks)にする」を参照してください。

カーネルスタックはページアウトされる可能性があるため、スタックベースのバッファー (つまりローカル変数) を DMA に渡すか、DISPATCH_LEVEL 以上で実行される任意のルーチンに渡すことに注意してください。

