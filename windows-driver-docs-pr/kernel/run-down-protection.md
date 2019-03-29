---
title: ランダウン防止
description: Windows XP 以降、run-down 保護はカーネル モード ドライバーを使用できます。 ドライバーは、run-down protection を使用して、作成され、別のカーネル モード ドライバーによって削除されている共有のシステム メモリ内のオブジェクトを安全にアクセスすることができます。
ms.assetid: AF451636-DBA0-4905-9723-73EE7AA9483E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d43014655454b20629cdda877bcc7e0cb6f792f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578430"
---
# <a name="run-down-protection"></a>ランダウン防止


Windows XP 以降、run-down 保護はカーネル モード ドライバーを使用できます。 ドライバーは、run-down protection を使用して、作成され、別のカーネル モード ドライバーによって削除されている共有のシステム メモリ内のオブジェクトを安全にアクセスすることができます。

オブジェクトはモード*実行*オブジェクトのすべての未処理のアクセスが完了し、新しい要求オブジェクトへのアクセスを許可しないかどうか。 たとえば、共有されたオブジェクトは、ように削除し、新しいオブジェクトに置き換え実行する必要があります。

共有オブジェクトを所有するドライバーには、取得および run-down 保護オブジェクトを解放するには、その他のドライバーが有効にすることができます。 完了すると場合 run-down 保護が有効で、所有者以外のドライバーが所有者にアクセスする前にオブジェクトが削除されるリスクを負うことがなくオブジェクトにアクセスできます。 アクセスが開始する前にへのアクセスのドライバーは、オブジェクトの run-down の保護を要求します。 有効期間が長いオブジェクトでは、この要求はほとんど常に付与します。 アクセスが完了すると、ドライバーへのアクセスは、オブジェクトの場合は、以前に取得した run-down 保護を解放します。

## <a name="primary-run-down-protection-routines"></a>プライマリ保護の run-down ルーチン


オブジェクトを共有するには、オブジェクトを所有するドライバーを呼び出し、 [ **ExInitializeRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569373)ルーチン run-down 保護オブジェクトを初期化するためにします。 この呼び出しの後、オブジェクトにアクセスするその他のドライバーを取得および run-down 保護オブジェクトを解放できます。

共有されたオブジェクトの呼び出しにアクセスするドライバー、 [ **ExAcquireRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569371)ルーチンをオブジェクトに run-down 保護を要求します。 アクセスが完了したら、このドライバーは呼び出し、 [ **ExReleaseRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569375) run-down 保護オブジェクトを解放するルーチン。

所有しているドライバー、認識された場合、共有されたオブジェクトを削除する必要がありますこのドライバーは、オブジェクトのすべての未処理のアクセスが完了するまでオブジェクトを削除するまで待機します。

共有オブジェクトを削除する準備として、所有しているドライバーを呼び出し、 [ **ExWaitForRundownProtectionRelease** ](https://msdn.microsoft.com/library/windows/hardware/jj569378)ルーチン実行するオブジェクトを待機します。 この呼び出し中に**ExWaitForRundownProtectionRelease** run-down 保護が解除されるオブジェクトの以前に許可したすべてのインスタンスの間、待機が防ぎます run-down 保護する、オブジェクトに新しい要求与えられます。 最後の保護されたアクセスを終了し、run-down 保護のすべてのインスタンスがリリースされると後、 **ExWaitForRundownProtectionRelease**から返されると、所有しているドライバーにより安全にオブジェクトが削除できます。

**ExWaitForRundownProtectionRelease** run-down 保護を共有されたオブジェクトに格納されるすべてのドライバーは、この保護をリリースするまで、呼び出し元のドライバーのスレッドの実行をブロックします。 防ぐために**ExWaitForRundownProtectionRelease** run-down 保護、オブジェクトの格納中に、中断されているが過度に長期間実行をブロックするには、共有オブジェクトにアクセスするスレッドをドライバーが避ける必要があります。 このため、ドライバーにアクセスする呼び出す必要があります**ExAcquireRundownProtection**と**ExReleaseRundownProtection**クリティカル領域または保護された領域は、内または IRQL での実行中に APC=\_レベル。

## <a name="uses-for-run-down-protection"></a>Run-down 保護の使用方法


Run-down 保護はほぼ常に利用が削除され、交換する必要がある場合によっては、共有されたオブジェクトへのアクセスを提供するために特に便利です。 呼び出しルーチンでは、このオブジェクトが削除後、オブジェクトへのアクセスに試みる必要がありますいないまたはデータ アクセス ドライバーです。 それ以外の場合、予期しない動作、データの破損、またはシステムの障害もこれらの無効なアクセスがあります。

たとえば、ウイルス対策のドライバー通常まだメモリに読み込まれたオペレーティング システムが実行されている場合。 場合によっては、このドライバーをアンロードし、ドライバーの更新されたリリースで置き換える必要があります。 その他のドライバーでは、このドライバーでルーチン、データにアクセスするウイルス対策のドライバーを I/O 要求を送信します。 I/O 要求を送信する前に、ファイル システム フィルター マネージャーなどのカーネル コンポーネントは、I/O 要求を処理するときに、ウイルス対策のドライバーの早期アンロードを防ぐ run-down の保護を取得できます。 I/O 要求が完了した後、run-down 保護を解放できます。

Run-down 保護は、共有されたオブジェクトへのアクセスをシリアル化できません。 アクセスする 2 つ以上のドライバーは同時に、そのオブジェクトに対する run-down 保護を保持し、オブジェクトへのアクセスをシリアル化する必要がありますの場合は、アクセスをシリアル化する相互排他ロックなど、他のいくつかのメカニズムを使用する必要があります。

## <a name="the-exrundownref-structure"></a>EX\_ランダウン\_REF 構造体


[ **EX\_ランダウン\_REF** ](https://msdn.microsoft.com/library/windows/hardware/jj569379)構造が共有されたオブジェクトの run-down 対策の状態を追跡します。 この構造体は、ドライバーに対して非透過的です。 Run-down 保護のシステム指定のルーチンでは、オブジェクト上で有効な現在の run-down 保護インスタンスの数をカウントするのにこの構造体を使用します。 これらのルーチンは、オブジェクトのが実行またはで実行されているプロセスではあるかどうかを追跡するためにもこの構造体を使用します。

オブジェクトを所有するドライバーを呼び出すオブジェクトを共有するには、 **ExInitializeRundownProtection**初期化するために、 **EX\_ランダウン\_REF**構造に関連付けられている、オブジェクト。 初期化後は、所有しているドライバーが利用できるこの構造体オブジェクトへのアクセスを必要とするその他のドライバーにします。 アクセスのドライバーでは、この構造体を渡すパラメーターとして、 **ExAcquireRundownProtection**と**ExReleaseRundownProtection**の呼び出しを取得および run-down 保護オブジェクトを解放します。 所有しているドライバーのパラメーターとしてこの構造体を渡す、 **ExWaitForRundownProtectionRelease**呼び出し、オブジェクトを安全に削除されるよう実行するを待機します。

## <a name="comparison-to-locks"></a>ロックとの比較


Run-down 保護では、共有オブジェクトへの安全なアクセスを保証するためにいくつかの方法の 1 つです。 別の方法では、ソフトウェアの相互排他ロックを使用します。 ドライバーは、別のドライバーによってロックされているオブジェクトへのアクセスを必要とする場合、最初のドライバーは、ロックを解放する 2 つ目のドライバーを待つ必要があります。 ただし、獲得と解放により、パフォーマンス ボトルネックとなるし、ロックが大量のメモリを消費することができます。 正しく使用しないと、ロックが競合とデッドロックが発生する場合は、同じ共有オブジェクトのドライバーにあります。 検出し、通常はデッドロックを回避するための取り組みでは、大量のコンピューティング リソースの迂回が必要です。

ロックとは対照的は run-down 保護に比較的軽量な処理時間とメモリの要件があります。 単純な参照カウントは、オブジェクトのすべての未処理のアクセスが完了するまでに、オブジェクトの削除を延期することを確認するオブジェクトに関連付けられます。 この方法でアトミック、オブジェクトへの安全なアクセスを保証するためにインタロックされたハードウェア命令ソフトウェアの相互排他ロックではなく使用できます。 取得および解放 run-down 保護への呼び出しは、通常は非常に高速です。 Run-down の保護などの軽量のメカニズムを使用する利点を長い寿命を備え、多くのドライバーの間で共有されている共有オブジェクトの重要なことはできます。

## <a name="other-run-down-protection-routines"></a>その他の run-down 保護ルーチン


その他のいくつかの run-down 保護ルーチンは、前に説明した以外に使用できます。 これらの追加ルーチンは、一部のドライバーで使用される可能性があります。

[ **ExReInitializeRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569374)ルーチンが以前に使用できるように[ **EX\_ランダウン\_REF** ](https://msdn.microsoft.com/library/windows/hardware/jj569379)、新しいオブジェクトに関連する構造体し、run-down の保護をこのオブジェクトを初期化します。

[ **ExRundownCompleted** ](https://msdn.microsoft.com/library/windows/hardware/jj569377)日常的な更新プログラム、 **EX\_ランダウン\_REF**構造を示すために、関連オブジェクトの下の実行完了しました。

[ **ExAcquireRundownProtectionEx** ](https://msdn.microsoft.com/library/windows/hardware/jj569372)と[ **ExReleaseRundownProtectionEx** ](https://msdn.microsoft.com/library/windows/hardware/jj569376)ルーチンと似ています[ **ExAcquireRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569371)と[ **ExReleaseRundownProtection**](https://msdn.microsoft.com/library/windows/hardware/jj569375)します。 これら 4 つのルーチンでは、増分または run-down 保護の共有オブジェクト上で有効なインスタンスのカウントをデクリメントします。 一方**ExAcquireRundownProtection**と**ExReleaseRundownProtection**にインクリメントされ、1 つずつ、このカウントをデクリメント**ExAcquireRundownProtectionEx**と**ExReleaseRundownProtectionEx**にインクリメントされ、任意の量によって、カウントをデクリメントします。

 

 




