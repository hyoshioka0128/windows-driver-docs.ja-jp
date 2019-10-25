---
title: ランダウン防止
description: Windows XP 以降では、カーネルモードドライバーで実行時の保護を利用できます。 ドライバーは、別のカーネルモードドライバーによって作成および削除された共有システムメモリ内のオブジェクトに安全にアクセスするために、実行時の保護を使用できます。
ms.assetid: AF451636-DBA0-4905-9723-73EE7AA9483E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fdd043fe695b3ca8077921552c48ff3824ef3f72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838444"
---
# <a name="run-down-protection"></a>ランダウン防止


Windows XP 以降では、カーネルモードドライバーで実行時の保護を利用できます。 ドライバーは、別のカーネルモードドライバーによって作成および削除された共有システムメモリ内のオブジェクトに安全にアクセスするために、実行時の保護を使用できます。

オブジェクトの未処理のアクセスがすべて完了し、オブジェクトへの新しい要求が許可されない場合は、オブジェクトが*実行*されていると言います。 たとえば、共有オブジェクトを削除して新しいオブジェクトに置き換えることができるように、共有オブジェクトをダウンさせる必要がある場合があります。

共有オブジェクトを所有するドライバーは、他のドライバーがオブジェクトの実行時の保護を取得して解放できるようにすることができます。 実行時の保護が有効になっている場合、所有者以外のドライバーは、アクセスが完了する前に所有者がオブジェクトを削除するリスクを負うことなく、オブジェクトにアクセスできます。 アクセスが開始される前に、アクセスするドライバーは、オブジェクトに対して実行時の保護を要求します。 有効期間が長いオブジェクトの場合、この要求はほぼ常に許可されます。 アクセスが完了すると、アクセスするドライバーは、オブジェクトに対して以前に取得した実行停止保護を解放します。

## <a name="primary-run-down-protection-routines"></a>プライマリ実行時の保護ルーチン


オブジェクトの共有を開始するために、オブジェクトを所有するドライバーは、オブジェクトの実行時保護を初期化するために、 [**Ex/downprotection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializerundownprotection)ルーチンを呼び出します。 この呼び出しの後、オブジェクトにアクセスする他のドライバーは、オブジェクトの実行時の保護を取得して解放できます。

共有オブジェクトにアクセスするドライバーは、 [**ExAcquireRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirerundownprotection)ルーチンを呼び出して、オブジェクトの実行時保護を要求します。 アクセスが完了すると、このドライバーは[**ExReleaseRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaserundownprotection)ルーチンを呼び出して、オブジェクトの実行時保護を解放します。

所有しているドライバーが共有オブジェクトを削除する必要があると判断した場合、このドライバーはオブジェクトの未処理のアクセスがすべて終了するまで、オブジェクトの削除を待機します。

共有オブジェクトを削除する準備として、所有しているドライバーは、オブジェクトがダウンするのを待機するために、 [**Exwaitforrundownprotectionrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exwaitforrundownprotectionrelease)ルーチンを呼び出します。 この呼び出しの間、 **Exwaitforrundownprotectionrelease**は、解放されるオブジェクトに対して以前に許可されたすべてのインスタンスを待機しますが、オブジェクトに対する実行時の保護の新しい要求が許可されないようにします。 最後に保護されたアクセスが完了し、実行中のすべてのインスタンスが解放された後、 **Exwaitforrundownprotectionrelease**はを返し、所有するドライバーはオブジェクトを安全に削除できます。

**Exwaitforrundownprotectionrelease**は、共有オブジェクトに対して実行ダウン保護を保持するすべてのドライバーがこの保護を解放するまで、呼び出し元ドライバースレッドの実行をブロックします。 **Exwaitforrundownprotectionrelease**が過度に長時間実行されないようにするには、共有オブジェクトにアクセスするドライバースレッドが、オブジェクトに対する実行時の保護を保持したまま中断されないようにする必要があります。 このため、ドライバーへのアクセスでは、 **ExAcquireRundownProtection**と**ExReleaseRundownProtection**を、重要なリージョンまたは保護されたリージョン内で、または IRQL = APC\_レベルで実行中に呼び出す必要があります。

## <a name="uses-for-run-down-protection"></a>実行時の保護に使用


実行時の保護は、常に使用可能であるものの削除や置換が必要になる可能性がある共有オブジェクトへのアクセスを提供する場合に特に便利です。 データにアクセスするドライバー、またはこのオブジェクトのルーチンを呼び出すドライバーは、オブジェクトが削除された後にアクセスしようとすることはできません。 そうしないと、これらの無効なアクセスによって、予期しない動作、データの破損、またはシステム障害が発生する可能性があります。

たとえば、ウイルス対策ドライバーは、通常、オペレーティングシステムの実行中にメモリに読み込まれたままになります。 場合によっては、このドライバーをアンロードし、ドライバーの更新されたリリースに置き換える必要があります。 他のドライバーは、このドライバーのデータとルーチンにアクセスするために、i/o 要求をウイルス対策ドライバーに送信します。 I/o 要求を送信する前に、ファイルシステムフィルターマネージャーなどのカーネルコンポーネントは、実行時の保護を取得して、i/o 要求を処理している間にウイルス対策ドライバーのアンロードを防ぐことができます。 I/o 要求が完了すると、実行時の保護が解放されます。

実行時の保護では、共有オブジェクトへのアクセスはシリアル化されません。 2つ以上のアクセス可能なドライバーがオブジェクトに対して同時に実行された保護を保持でき、そのオブジェクトへのアクセスをシリアル化する必要がある場合は、相互排他ロックなど、他のメカニズムを使用してアクセスをシリアル化する必要があります。

## <a name="the-ex_rundown_ref-structure"></a>EX\_ランダウン\_REF 構造体


[**EX\_ランダウン\_REF**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体は、共有オブジェクトの実行時の保護状態を追跡します。 この構造は、ドライバーに対して非透過的です。 システムによって提供される実行時保護ルーチンは、この構造体を使用して、現在オブジェクトで有効になっている実行時保護のインスタンスの数をカウントします。 また、これらのルーチンは、この構造を使用して、オブジェクトが実行されているか、または実行中であるかを追跡します。

オブジェクトの共有を開始するには、オブジェクトを所有するドライバーが、オブジェクトに関連付けられている**EX\_ランダウン\_REF**構造体を初期化するために、 **Ex/downprotection**を呼び出します。 初期化後、所有するドライバーは、オブジェクトへのアクセスを必要とする他のドライバーがこの構造を使用できるようにすることができます。 アクセスするドライバーは、この構造体をパラメーターとして、オブジェクトの実行時保護を取得および解放する**ExAcquireRundownProtection**および**ExReleaseRundownProtection**呼び出しに渡します。 所有しているドライバーは、この構造体をパラメーターとして**Exwaitforrundownprotectionrelease**呼び出しに渡します。この呼び出しは、オブジェクトが実行されるのを待って、安全に削除できるようにします。

## <a name="comparison-to-locks"></a>ロックとの比較


実行時の保護は、共有オブジェクトへの安全なアクセスを保証するいくつかの方法の1つです。 もう1つの方法は、相互排他的なソフトウェアロックを使用することです。 ドライバーが、現在別のドライバーによってロックされているオブジェクトへのアクセスを必要とする場合、最初のドライバーは、2番目のドライバーがロックを解放するまで待機する必要があります。 ただし、ロックの取得と解放はパフォーマンスのボトルネックになる可能性があり、ロックは大量のメモリを消費する可能性があります。 正しく使用しないと、同じ共有オブジェクトに対して競合するドライバーがデッドロック状態になる可能性があります。 デッドロックを検出して回避するには、通常、大量のコンピューティングリソースを diversion する必要があります。

ロックとは対照的に、実行時の保護には比較的軽量の処理時間とメモリの要件があります。 オブジェクトのすべての未処理のアクセスが完了するまで、オブジェクトの削除が遅延されるようにするために、オブジェクトには単純な参照カウントが関連付けられています。 この方法を使用すると、相互排他的なソフトウェアロックの代わりにアトミックでインタロックされたハードウェア命令を使用して、オブジェクトへの安全なアクセスを保証できます。 通常、取得と解放の実行のための呼び出しは非常に高速です。 実行時間の長い共有オブジェクトでは、長期間の保護機能を使用する利点があり、多くのドライバー間で共有されている場合があります。

## <a name="other-run-down-protection-routines"></a>その他の実行時の保護ルーチン


前に説明したものに加えて、他のいくつかの実行時保護ルーチンも使用できます。 これらの追加ルーチンは、一部のドライバーで使用される場合があります。

[**Exreinitializer Erundownprotection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializerundownprotection)ルーチンを使用すると、以前に使用した[ **\_ランダウン\_REF**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体を新しいオブジェクトに関連付けることができ、このオブジェクトの実行時の保護が初期化されます。

[**Exrundowncompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exrundowncompleted)ルーチンは、 **EX\_ランダウン\_REF**構造体を更新して、関連付けられているオブジェクトの実行が完了したことを示します。

[**ExAcquireRundownProtectionEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirerundownprotectionex)ルーチンと[**ExReleaseRundownProtectionEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaserundownprotectionex)ルーチンは、 [**ExAcquireRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirerundownprotection)と[**ExReleaseRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaserundownprotection)に似ています。 これらの4つのルーチンは、共有オブジェクトに対して有効な実行時保護のインスタンスの数をインクリメントまたはデクリメントします。 **ExAcquireRundownProtection**と**ExReleaseRundownProtection**は、このカウントを1つずつ増減し、 **ExAcquireRundownProtectionEx**と**ExReleaseRundownProtectionEx**をインクリメントし、カウントをデクリメントします。任意の金額。

 

 




