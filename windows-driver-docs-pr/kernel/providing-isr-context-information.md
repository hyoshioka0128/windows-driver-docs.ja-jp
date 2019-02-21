---
title: ISR コンテキスト情報を提供します。
description: ISR コンテキスト情報を提供します。
ms.assetid: 216c3111-3638-4410-a720-ff3d65a1eadd
keywords:
- 割り込みサービス ルーチン WDK カーネル、コンテキスト情報
- Isr WDK カーネルでは、コンテキスト情報
- 割り込みオブジェクト WDK カーネル、コンテキスト情報
- コンテキスト情報 WDK の割り込み
- ポインターの WDK の割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e9720effb5636681dae6881c775d6e55c6178d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531007"
---
# <a name="providing-isr-context-information"></a>ISR コンテキスト情報を提供します。





エントリの ISR はドライバーを設定することが呼び出されたときにどのようなコンテキスト領域へのポインターを受け取る[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)ルーチンを登録します。

ほとんどのドライバーは、割り込みを生成する物理デバイスを表すデバイス オブジェクトまたはそのデバイス オブジェクトのデバイスの拡張機能にコンテキスト ポインターを設定します。 デバイス拡張機能では、ドライバーがドライバーの ISR の状態情報を格納できますと[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン、後者のうち、通常はほぼすべてを満たす各 I/O 処理の要求中断するデバイスを発生します。

通常、ドライバーの各デバイスの割り込みのオブジェクトへのポインターを格納するデバイスの拡張機能を使用して、(への呼び出しから返された**IoConnectInterruptEx**)。 ドライバーは、ISR、割り込みが ISR サポートしているデバイスによって発行されたかどうかを判断することができるデバイスの拡張機能にも通常情報を格納します。

(または、割り込みオブジェクト ポインターは、ドライバーによって割り当てられる非ページ プールに格納できます。)

 

 




