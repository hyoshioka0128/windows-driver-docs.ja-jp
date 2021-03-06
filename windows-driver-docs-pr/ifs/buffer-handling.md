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

-   アドレスで、高ビットが設定されていることを確認しています。 これでは機能しません、システムは、4 ギガバイト チューニング (4 gt) を使用している x86 ベースのコンピューター上で、Boot.ini ファイルで/3 GB オプションを設定します。 その場合は、ユーザー モードのアドレスは、アドレス空間の 3 つ目のギガバイト (GB) の上位ビットを設定します。

-   使用して[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)と[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)アドレスを検証します。 ユーザー モードの有効なアドレスのアドレスは、プローブ時に、これにより、中に何もないプローブ操作後に有効のままにする必要があります。 したがって、この手法では、定期的な再現がクラッシュする可能性のある微妙な競合状態が導入されています。 **ProbeForRead**と**ProbeForWrite**呼び出しは、別の理由のために必要な: はユーザー モード アドレスかどうかと、バッファーの長さは、ユーザーのアドレス範囲内で、検証します。 によってキャッチしませんが、有効なカーネル モードのアドレスのユーザーを渡すことができます、プローブを省略した場合、 \_\_お試しくださいと\_\_ブロック (構造化例外処理) を除くし、大きなセキュリティ ホールが開きます。 したがって**ProbeForRead**と**ProbeForWrite**呼び出しは配置と、ユーザー モード アドレスに加えて、長さが、ユーザーのアドレスの範囲内にあることを確認するために必要です。 ただし、 \_\_お試しくださいと\_\_ブロックがアクセスを防ぐために必要な点が異なります。

    なお[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)のみを検証する (わずか 2 GB 未満の例では、4 gt ことがなくシステム)、可能なユーザー モード アドレスの範囲内のアドレスと長さの fall いないかどうか、メモリアドレスは有効です。 これに対し、 [ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)これらが有効なメモリ アドレスであることを確認する指定された長さの各ページの最初のバイトへのアクセスを試みます。

-   メモリ マネージャーの機能に依存 ([**MmIsAddressValid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmisaddressvalid)など)、アドレスが有効であることを確認します。 プローブの関数と同様、再現がクラッシュする可能性のある競合状態が導入されます。

-   構造化例外処理の使用の失敗。 \_\_お試しくださいと\_\_コンパイラ内の関数では、オペレーティング システム レベルのサポートを使用して、例外処理の点が異なります。 カーネル レベルでの例外は呼び出すことによってバックアップ スロー [ **ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus)、または、関連する関数の 1 つ。 バグ チェックにより、構造化例外処理、例外を発生させる可能性がありますすべての呼び出しの周りの使用に失敗するドライバー (通常 KMODE\_例外\_いない\_処理済み)。

    構造化例外処理が、エラーが発生する予期しないコードの周りを使用するの間違いであるに注意してください。 これは、だけマスク実際バグを見つけるとします。 配置すること、 \_\_お試しくださいと\_\_を除き、ラッパー ルーチンのディスパッチの最上位レベルではありません、この問題に適切なソリューションが、ドライバー作成者が試みたリフレックス ソリューションがあります。

-   残っている安定したユーザーのメモリの内容に依存します。 たとえば、ドライバーが、ユーザー モードのメモリ位置に値を書き込むし、同じルーチンで、後でそのメモリ位置を参照してください。 悪意のあるアプリケーションでしたそのメモリを積極的に変更し、クラッシュするドライバーにより、その結果。

ファイル システムでは、これらの問題、特に重大なユーザー バッファーに直接アクセスする時に通常依存しているため (メソッド\_どちらも転送方法)。 このようなドライバーは、ユーザーのバッファーを直接操作し、オペレーティング システム レベルのクラッシュを回避するためをバッファー処理のための予防措置のメソッドに組み込む必要がありますので。 ドライバーは、高速の I/O がサポートされている場合のような問題からは保護する必要があります、高速の I/O は常に、生のメモリ ポインターを渡します。

WDK には FASTFAT と cdfs を含むファイル システムのサンプル コード、バッファーの検証の多くの例が含まれていますを含みます。

-   **FatLockUserBuffer** fastfat 関数\\deviosup.c 使用[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)ユーザー バッファーの背後にある物理ページをロックダウンして[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で**FatMapUserBuffer**がロックされているページに仮想のマッピングを作成します。

-   **FatGetVolumeBitmap** fastfat 関数\\fsctl.c 使用[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)と[ **ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)デフラグ API でユーザーのバッファーを検証します。

-   **CdCommonRead** cdf 関数\\read.c 使用\_\_お試しくださいと\_\_ゼロ ユーザー バッファーへのコードの周りを除きます。 サンプルのコードで注意**CdCommonRead** try を使用して、キーワードを除くが表示されます。 コンパイラの拡張機能の観点から、WDK 環境で C でのこれらのキーワードが定義されている\_\_お試しくださいと\_\_を除く。 ネイティブ コンパイラ型を使用して、例外を適切に処理する必要があります C++ コードを使用してすべてのユーザーとして\_ \_try は C++ のキーワードが C キーワードではなく、およびカーネル ドライバーに対して有効でない C++ 例外処理の形式を提供します。

 

 




