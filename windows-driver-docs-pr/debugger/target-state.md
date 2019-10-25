---
title: ターゲットの状態
description: ターゲットの状態
ms.assetid: befd6c0b-dd16-40a1-bc6b-634b354d2a75
keywords:
- デバッガーエンジン API、ターゲット、状態
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a80216ad6961bb5f3df2773634a1e5775de532e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834272"
---
# <a name="target-state"></a>ターゲットの状態


メソッド[**outputcurrentstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputcurrentstate) 、ターゲットの現在の状態をデバッガーの出力ストリームに出力します。

ターゲットの現在の実行状態は、 [**Getexecutionstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexecutionstatus)によって返されます。 ターゲットが中断されている場合は、 [**Setexecutionstatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexecutionstatus)メソッドを使用して、実行モードのいずれかで実行を再開できます。

[**GetReturnOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getreturnoffset)メソッドは、現在の関数から制御が戻ったときに実行される命令のアドレスを返します。

[**GetNearInstruction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnearinstruction)は、指定されたアドレスを基準とする命令の位置を返します。

### <a name="span-idexamining_the_stack_tracespanspan-idexamining_the_stack_tracespanexamining-the-stack-trace"></a><span id="examining_the_stack_trace"></span><span id="EXAMINING_THE_STACK_TRACE"></span>スタックトレースを調べています

*呼び出し履歴*には、スレッドによって行われる関数呼び出しのデータが含まれます。 各関数呼び出しのデータは*スタックフレーム*と呼ばれ、戻りアドレス、関数に渡されるパラメーター、および関数のローカル変数が含まれます。 関数呼び出しが行われるたびに、新しいスタックフレームがスタックの一番上にプッシュされます。 この関数が戻ると、スタックフレームがスタックからポップされます。 各スレッドには、そのスレッドで行われた呼び出しを表す独自の呼び出し履歴があります。

関数呼び出しのすべてのデータがスタックフレームに格納されるわけではない   に**注意**してください。 パラメーターとローカル変数は、一度にレジスタに格納できます。

 

呼び出し履歴または*スタックトレース*を取得するには、 [**GetStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)および[**GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace)メソッドを使用します。 スタックトレースは、 [**OutputStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)と[**OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)を使用して出力できます。

 

 





