---
title: バッファー処理
description: バッファー処理
ms.assetid: 0739ff35-2915-4237-9fe0-11559eccb0bb
keywords:
- 脅威を最小限に抑え、セキュリティ WDK ファイル システム
- WDK のバッファーはファイル システム
- ページ バッファ WDK ファイル システム
- 非ページング バッファー WDK ファイル システム
- バグ チェック WDK ファイル システム
- アドレス検証 WDK ファイル システム
- 高速の I/O の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 931afa660e500a7bbabbac3db35684e75792b3ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369290"
---
# <a name="buffer-handling"></a>バッファー処理


## <span id="ddk_buffer_handling_if"></span><span id="DDK_BUFFER_HANDLING_IF"></span>


おそらく、ドライバー内で最も一般的なエラーは、バッファーが無効か、小さすぎるのバッファー処理に関連します。 これらのエラーでは、バッファー オーバーフローを許可したり、システムのクラッシュは、構成システムのセキュリティ侵害が発生することができます。

ドライバーの観点から、バッファーは、2 種類のいずれかで送られてきます。

-   バッファーは、可能性のあるメモリに常駐していることができない可能性がありますをページングします。

-   非ページ、バッファー メモリに常駐している必要があります。

もちろん、無効なアドレスはページングも、nonpaged ですがオペレーティング システムをそのようなバッファー ページ フォールトの原因を解決するための機能は、"standard"のアドレス範囲 (ページ カーネル アドレスのいずれかに無効なアドレスが分離されます。非ページ カーネル アドレス、またはユーザーのアドレス) と、適切な種類のエラーを生成します。 バッファーのエラーの処理かのバグ チェックが常に (ページ\_フォールト\_IN\_非ページ\_領域で、たとえば) または、例外によって (状態\_アクセス\_例については、違反)。 バグ チェックでは、場合、システムは、操作を停止します。 例外の場合、スタック ベースの例外ハンドラーが呼び出され、例外を処理しない場合、バグ チェックが呼び出されます。

関係なく、バグ チェックをリーダーになるドライバーが原因となるアプリケーション プログラムによって呼び出すことができ、アクセス パスでは、ドライバー内でのセキュリティ違反です。 これにより、システム全体にサービス拒否攻撃が発生するアプリケーションです。

この領域で最も一般的な問題の 1 つは、ドライバー作成者が想定は運用環境に関するが多すぎることです。 以下に示します。

-   アドレスで、高ビットが設定されていることを確認しています。 これでは機能しません、システムは、4 ギガバイト チューニング (4GT) を使用している x86 ベースのコンピューター上で、Boot.ini ファイルで /3GB オプションを設定します。 その場合は、ユーザー モードのアドレスは、アドレス空間の 3 つ目のギガバイト (GB) の上位ビットを設定します。

-   [ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)と[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite) を使用してアドレスを検証します。 これは、プローブ時のアドレスが有効なユーザー モードアドレスであることが保証されますが、プローブ操作後もアドレスを有効のままにする必要はありません。 したがって、この手法では、再現性のない定期的なクラッシュを引き起こす可能性のある微妙な競合状態が発生します。 **ProbeForRead**と**ProbeForWrite**呼び出しは、別の理由で必要です。アドレスがユーザー モードアドレスであるかかどうかと、バッファーの長さが、ユーザーのアドレス範囲内であるかどうかを検証します。 によってキャッチしませんが、有効なカーネル モードのアドレスのユーザーを渡すことができます、プローブを省略した場合、 \_\_お試しくださいと\_\_ブロック (構造化例外処理) を除くし、大きなセキュリティ ホールが開きます。
プローブを省略した場合、ユーザーは有効なカーネル モードのアドレスのを渡すことができます、これは、\_\_try と\_\_except ブロック (構造化例外処理) でキャッチされず、大きなセキュリティ ホールを開きます。 したがって**ProbeForRead**と**ProbeForWrite**呼び出しはアラインメントを保証し、ユーザー モード アドレスに加えて、長さをユーザーのアドレスの範囲内に収めるために必要です。 ただし、アクセスを防ぐためには、 \_\_try と\_\_except ブロックが必要です。

    なお[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)のみを検証する (わずか 2 GB 未満の例では、4 gt ことがなくシステム)、可能なユーザー モード アドレスの範囲内のアドレスと長さの fall いないかどうか、メモリアドレスは有効です。 これに対し、 [ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)これらが有効なメモリ アドレスであることを確認する指定された長さの各ページの最初のバイトへのアクセスを試みます。

-   メモリ マネージャーの機能に依存 ([**MmIsAddressValid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmisaddressvalid)など)、アドレスが有効であることを確認します。 プローブの関数と同様、再現がクラッシュする可能性のある競合状態が導入されます。

-   構造化例外処理の使用の失敗。 コンパイラ内の \_\_try と\_\_except 関数は、例外処理のためにオペレーティング システム レベルのサポートを使用します。 カーネル レベルでの例外は [ **ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus)、または、関連する関数のいずれかを呼び出すことによってスローバックされます。 ドライバーは、例外を発生させる可能性のある呼び出しで構造化例外処理をしないと、バグ チェック(通常 KMODE\_ EXCEPTION \_ NOT \_ HANDLED)につながります。

    エラーの発生が予想されないコードの周囲で構造化例外処理を使用するの間違いです。 これは、そうでなければ発見されるであろう実際のバグをマスクするだけです。 ルーチンの最上位のディスパッチレベルに、\_\_try と\_\_exceptを配置することは、この問題の適切なソリューションではありませんが、ドライバー作成者が試みるリフレックス ソリューションである場合があります。

-   残っている安定したユーザーのメモリの内容に依存します。 たとえば、ドライバーが、ユーザー モードのメモリ位置に値を書き込むし、同じルーチンで、後でそのメモリ位置を参照してください。 悪意のあるアプリケーションでしたそのメモリを積極的に変更し、クラッシュするドライバーにより、その結果。

ファイル システムでは、これらの問題、特に重大なユーザー バッファーに直接アクセスする時に通常依存しているため (メソッド\_どちらも転送方法)。 このようなドライバーは、ユーザーのバッファーを直接操作し、オペレーティング システム レベルのクラッシュを回避するためをバッファー処理のための予防措置のメソッドに組み込む必要がありますので。 ドライバーは、高速の I/O がサポートされている場合のような問題からは保護する必要があります、高速の I/O は常に、生のメモリ ポインターを渡します。

WDK には FASTFAT と cdfs を含むファイル システムのサンプル コード、バッファーの検証の多くの例が含まれていますを含みます。

-   **FatLockUserBuffer** fastfat 関数\\deviosup.c 使用[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)ユーザー バッファーの背後にある物理ページをロックダウンして[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で**FatMapUserBuffer**がロックされているページに仮想のマッピングを作成します。

-   **FatGetVolumeBitmap** fastfat 関数\\fsctl.c 使用[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)と[ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)デフラグ API でユーザーのバッファーを検証します。

-   cdfs \\ read.c の **CdCommonRead** 関数は、ユーザーバッファーをゼロにするコードの周りで \_\_try と \_\_except を使用します。 **CdCommonRead** のサンプルのコードでは、try キーワードと except キーワードを使用しているように見えることに注意してください。 WDK 環境では、C でのこれらのキーワードはコンパイラの拡張機能 \_\_try と\_\_exceptによって定義されています。 \_\_try は C++ のキーワードであり、 C キーワードではないため、C++ コードを使用するユーザーはネイティブ コンパイラ型を使用して、例外を適切に処理する必要があり、カーネル ドライバーに対して有効でない C++ 例外処理の形式を提供します。

 

 




