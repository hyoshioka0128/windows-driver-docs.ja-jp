---
title: ターゲットの状態
description: ターゲットの状態
ms.assetid: befd6c0b-dd16-40a1-bc6b-634b354d2a75
keywords:
- デバッガーのエンジンの API、ターゲット、状態
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 058e1649f6741d354797932948592c9bd621bde1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368649"
---
# <a name="target-state"></a>ターゲットの状態


メソッド[ **OutputCurrentState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputcurrentstate)デバッガーの出力ストリームにターゲットの現在の状態が出力されます。

ターゲットの現在の実行状態がによって返される[ **GetExecutionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexecutionstatus)します。 ターゲットが中断されている場合、メソッド[ **SetExecutionStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexecutionstatus)実行モードのいずれかの実行を再開するために使用できます。

メソッド[ **GetReturnOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getreturnoffset)現在の関数が返されるときに実行される命令のアドレスを返します。

[**GetNearInstruction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnearinstruction)命令を特定のアドレスに対する相対の位置を返します。

### <a name="span-idexaminingthestacktracespanspan-idexaminingthestacktracespanexamining-the-stack-trace"></a><span id="examining_the_stack_trace"></span><span id="EXAMINING_THE_STACK_TRACE"></span>スタック トレースを調べる

A*コール スタック*スレッドによって行われる関数呼び出しのデータが含まれています。 各関数呼び出しのデータと呼びます、*スタック フレーム*戻り値のアドレスでは、関数、および関数のローカル変数に渡されるパラメーターが含まれています。 関数呼び出しが行われるたび、新しいスタック フレームは、スタックの一番上にプッシュされます。 その関数から制御が戻るときに、スタック フレームはスタックからポップします。 各スレッドは、そのスレッドで行われた呼び出しを表す独自のコール スタックを持っています。

**注**  関数呼び出しのデータのすべてのスタック フレームに格納できます。 パラメーターと、ローカル変数をレジスタに格納することができます。

 

呼び出し履歴を取得するまたは*スタック トレース*、メソッドを使用して[ **GetStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)と[ **GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace). スタック トレースを使用して印刷できる[ **OutputStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)と[ **OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)します。

 

 





