---
title: ユーザー領域とシステム領域
description: ユーザー領域とシステム領域
ms.assetid: 2d988178-cd19-4dc4-8dc1-39b9b6a1aaad
keywords:
- システムの領域
- システムの領域のアドレス
- システムの領域でのブレークポイント
- カーネル領域
- カーネル領域、アドレス
- カーネル領域、ブレークポイント
- ユーザーの領域
- アドレスのユーザー領域
- ブレークポイントのユーザー領域
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: afa8db8bef2370d36aa4d0038b6ec0d34c1f55ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549773"
---
# <a name="user-space-and-system-space"></a>ユーザー領域とシステム領域


Windows では、各ユーザー モード アプリケーションに、仮想アドレスのブロックが与えられます。 これと呼ばれますが、*ユーザー空間*そのアプリケーションの。 呼ばれるアドレスの他の大きなブロック*システム領域*または*カーネル領域*アプリケーションが直接アクセスできません。

WinDbg または CDB が設定した場合、[ブレークポイント](using-breakpoints.md)ユーザー領域でこのブレークポイントが 1 つのプロセスのユーザー領域で指定したアドレスに設定します。 ユーザー モードのデバッグは、中には、現在のプロセスは、仮想アドレスの意味を決定します。 詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

カーネル モードでのユーザー領域でブレークポイントを設定することができます、 **bp**、 **bu**、および**ba**コマンド、または、**ブレークポイント** ダイアログ ボックス。 最初に使用する必要があります、*プロセス コンテキスト*を使用してそのアドレス空間を所有するユーザー モード プロセスを指定する **.process/i** (またはプロセスに固有のブレークポイント一部カーネル領域関数) を切り替える、正しいターゲット[プロセス コンテキスト](changing-contexts.md#process-context)します。

ユーザー領域内のブレークポイントは、ブレークポイントが設定されたときに、コンテキストを持つプロセスがアクティブなプロセスに関連付けられた、常に。 ユーザー モード デバッガーがこのプロセスをデバッグし、カーネル デバッガーがデバッグで、プロセスが実行されているコンピューターの場合、このブレークポイントは、ブレークポイントがカーネル デバッガーから実際に設定されていても、ユーザー モード デバッガーに分割します。 この時点では、カーネル デバッガーからシステムに侵入したり、使用して、 [ **.breakin (カーネル デバッガーにブレーク)** ](-breakin--break-to-the-kernel-debugger-.md)カーネル デバッガーに制御を転送するユーザー モード デバッガーからコマンド。

### <a name="span-iddeterminingtherangeofuserspaceandsystemspacespanspan-iddeterminingtherangeofuserspaceandsystemspacespandetermining-the-range-of-user-space-and-system-space"></a><span id="determining_the_range_of_user_space_and_system_space"></span><span id="DETERMINING_THE_RANGE_OF_USER_SPACE_AND_SYSTEM_SPACE"></span>範囲のユーザー領域とシステム領域を決定します。

使用することがユーザーの領域と、ターゲット コンピューター上のシステム領域の程度を判断する必要がある場合、 [ **dp (メモリの表示)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) Windowsグローバル変数を表示するカーネルデバッガーからコマンド**MmHighestUserAddress**します。 この変数には、ユーザーの領域の最上位のアドレスが含まれています。 システム領域のアドレスは常にユーザー領域のアドレスよりも高いため、この値を使用すると、任意指定のアドレスがユーザー領域で、またはカーネル領域がかどうかを判断します。

X86 32 ビット ターゲット コンピューターでなどのプロセッサと標準のブート パラメーターでは、このコマンドは、次の結果が表示されます。

```dbgcmd
kd> dp nt!mmhighestuseraddress L1 
81f71864  7ffeffff 
```

これは、0x00000000 に 0x7FFEFFFF アドレスからユーザー領域の範囲をシステムの領域の最上位のアドレス (つまり、標準の 32 ビット Windows のインストールで 0 xffffffff) まで 0x80000000 したがって範囲を示します。

64 ビット ターゲットのコンピューターとは異なる値が発生します。 たとえば、このコマンドは、次の表示可能性があります。

```dbgcmd
0: kd> dp nt!mmhighestuseraddress L1 
fffff800`038b4010  000007ff`fffeffff 
```

これは、0x00000000 からのユーザー領域の範囲を示します\`00000000 に 0x000007FF\`FFFEFFFF します。 そのため、システムの領域が 0x00000800 からすべてのアドレスが含まれます\`00000000 上昇します。

Windows のメモリ管理の詳細については、次を参照してください。 *Microsoft Windows internals 』* David Solomon、Mark Russinovich (4 th edition、Microsoft Press、2005)。

 

 





