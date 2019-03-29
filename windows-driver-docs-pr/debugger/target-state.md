---
title: ターゲットの状態
description: ターゲットの状態
ms.assetid: befd6c0b-dd16-40a1-bc6b-634b354d2a75
keywords:
- デバッガーのエンジンの API、ターゲット、状態
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1881d6ab03e7f163c1ffa7dbfe9639ff7e63b393
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572520"
---
# <a name="target-state"></a>ターゲットの状態


メソッド[ **OutputCurrentState** ](https://msdn.microsoft.com/library/windows/hardware/ff553206)デバッガーの出力ストリームにターゲットの現在の状態が出力されます。

ターゲットの現在の実行状態がによって返される[ **GetExecutionStatus**](https://msdn.microsoft.com/library/windows/hardware/ff546675)します。 ターゲットが中断されている場合、メソッド[ **SetExecutionStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff556693)実行モードのいずれかの実行を再開するために使用できます。

メソッド[ **GetReturnOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff548237)現在の関数が返されるときに実行される命令のアドレスを返します。

[**GetNearInstruction** ](https://msdn.microsoft.com/library/windows/hardware/ff547197)命令を特定のアドレスに対する相対の位置を返します。

### <a name="span-idexaminingthestacktracespanspan-idexaminingthestacktracespanexamining-the-stack-trace"></a><span id="examining_the_stack_trace"></span><span id="EXAMINING_THE_STACK_TRACE"></span>スタック トレースを調べる

A*コール スタック*スレッドによって行われる関数呼び出しのデータが含まれています。 各関数呼び出しのデータと呼びます、*スタック フレーム*戻り値のアドレスでは、関数、および関数のローカル変数に渡されるパラメーターが含まれています。 関数呼び出しが行われるたび、新しいスタック フレームは、スタックの一番上にプッシュされます。 その関数から制御が戻るときに、スタック フレームはスタックからポップします。 各スレッドは、そのスレッドで行われた呼び出しを表す独自のコール スタックを持っています。

**注**  関数呼び出しのデータのすべてのスタック フレームに格納できます。 パラメーターと、ローカル変数をレジスタに格納することができます。

 

呼び出し履歴を取得するまたは*スタック トレース*、メソッドを使用して[ **GetStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff548425)と[ **GetContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff545748). スタック トレースを使用して印刷できる[ **OutputStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff553252)と[ **OutputContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff553203)します。

 

 





