---
title: スピンロックの概要
description: スピンロックの概要
ms.assetid: a37c0db4-ff9c-4958-a9f4-62b671458d03
keywords:
- KSPIN_LOCK
- executive スピン ロック WDK カーネル
- 割り込みスピン ロック WDK カーネル
- スピン ロック WDK カーネルをキューに登録
- スピン ロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cb62577c53d3b6a4fbde51b76e38649f2b2029e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536519"
---
# <a name="introduction-to-spin-locks"></a>スピンロックの概要





スピン ロックは、カーネル定義のカーネル モードのみの同期メカニズム、不透明な型としてエクスポートします。KSPIN\_ロックします。 同時に、IRQL で実行できるルーチンによって同時アクセスから共有データまたはリソースを保護する、スピン ロックを使用できます&gt;= ディスパッチ\_SMP マシン内のレベル。

多くのコンポーネントは、ドライバーを含めて、スピン ロックを使用します。 任意の種類のドライバーが 1 つ以上使用可能性があります*executive スピン ロック*します。 たとえば、ほとんどのファイル システムでは、Irp の処理が、ファイル システムのワーカー スレッド コールバック ルーチンと FSD の両方を格納するのに、インタロックされた作業のキュー、ファイル システム ドライバー (FSD) でデバイスの拡張機能を使用します。 インタロックされた作業をキューは、キューや Irp を削除しようとして同時にすべてのスレッドに Irp を挿入しようとしています。 FSD 間の競合を解決する、executive スピン ロックによって保護されます。 別の例としては、システムのフロッピー コント ローラー ドライバーは、2 つの executive スピン ロックを使用します。 Executive スピン ロックを 1 つは、インタロックされた作業キューがこのドライバーのデバイス専用のスレッドと共有を保護します。他は、次の 3 つのドライバー ルーチンによって共有されるタイマー オブジェクトを保護します。

Microsoft Windows XP および Windows の以降のバージョンのドライバーを使用できる[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)と[ **KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)取得およびとしてスピン ロックを解放する、*スピン ロックをキューに置かれた*します。 キューに置かれたスピン ロックでは、マルチプロセッサ コンピューターで通常スピンロックの競合が増加のロックよりも優れたパフォーマンスを提供します。 詳細については、次を参照してください。[スピン ロックをキューに置かれた](queued-spin-locks.md)します。 Windows 2000 用のドライバーを使用できる[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)と[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)取得およびとして、通常、スピン ロックを解放するにはスピン ロックします。

単純なデータ構造へのアクセスを同期するには、ドライバーはいずれかの使用、 **ExInterlocked * Xxx*** ルーチン データ構造をアトミックにアクセスできるようにします。 これらのルーチンを使用するドライバーは、取得するか、スピン ロックを明示的に解放する必要はありません。

ISR のあるすべてのドライバーを使用して、*スピン ロックを中断*のデータやその ISR 間で共有されるハードウェアを保護してその[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチンは、通常呼び出される、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)と[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン。 割り込みのスピン ロックは、ドライバーを呼び出すときに作成される割り込みオブジェクトのセットに関連付けられて[ **IoConnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff548371)」の説明に従って、ISR. を登録します。

**ドライバーでスピン ロックを使用して次のガイドラインに従います。**

-   記憶域を使用して、任意のデータまたはスピン ロックで保護されたリソースと常駐システム容量のメモリ内の対応する、スピン ロック (ように、非ページ プール、[スペースの仮想メモリと物理メモリ](overview-of-windows-memory-space.md)図)。 ドライバーを使用して executive スピン ロックをストレージを提供する必要があります。 ただし、デバイス ドライバー必要がありますいない、記憶域を提供、割り込みスピン ロック multivector ISR または 1 つ以上の ISR がある場合を除き、ISR. を登録する」の説明に従って

-   呼び出す[ **KeInitializeSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff552160)ドライバーが、保護されるリソースまたは共有データへのアクセスを同期するために使用する前に記憶域を提供する各スピン ロックを初期化します。

-   一般的に、適切な IRQL でスピン ロックを使用するすべてのサポート ルーチンを呼び出す&lt;= ディスパッチ\_executive スピン ロックのレベル&lt;ドライバーの割り込みのオブジェクトに関連付けられている割り込みスピンロックの DIRQL を = です。

-   スピン ロックを保持するときに、可能な限り早く実行するルーチンを実装します。 25 (マイクロ秒) よりも長いスピン ロックを保持する必要がありますルーチンにはありません。

-   スピン ロックを保持する際に、次のいずれかを実行するルーチンを実装しません。

    -   ハードウェア例外が発生またはソフトウェア例外が発生します。

    -   ページング可能なメモリにアクセスしようとしてください。

    -   デッドロックが発生する場合や、スピン ロックを保持する 25 マイクロ秒を超える可能性がありますを再帰的な呼び出しを作成します。

    -   デッドロックが発生する可能性がありますいる場合は、別のスピン ロックを取得しようとしてください。

    -   上記の規則に違反する外部ルーチンを呼び出します。

 

 




