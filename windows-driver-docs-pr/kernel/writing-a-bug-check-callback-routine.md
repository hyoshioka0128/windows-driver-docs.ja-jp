---
title: バグ チェック コールバック ルーチンの記述
description: バグ チェック コールバック ルーチンの記述
ms.assetid: 62aefe67-e197-4c45-b994-19bd7369dbc1
keywords:
- バグ チェック コールバック ルーチン WDK カーネル
- コールバック ルーチン WDK のバグ チェック
- コールバック ルーチンを登録します。
- KeRegisterBugCheckCallback
- BugCheckCallback
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 25eb6905403a466cc432ef83feb8af639018ea8b
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106424"
---
# <a name="writing-a-bug-check-reason-callback-routine"></a>バグ チェックのためのコールバック ルーチンを記述します。

ドライバーは、システムのバグ チェックが発行するときに実行されるコールバック ルーチンを登録できます。 ドライバーは、バグ チェック コールバック ルーチンを使用して、自分のデバイスを既知の状態にリセットします。

Windows でシステムの呼び出し、 [ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)クラッシュ ダンプ ファイルが書き込まれた後に、コールバック関数。

クラッシュ ダンプ ファイルをセカンダリ データを書き込む、KBUGCHECK_REASON_CALLBACK_ROUTINE を使用できます。
 
ドライバーは、クラッシュ ダンプ ファイルにドライバー固有のデータ ページを追加の KBUGCHECK_REASON_CALLBACK_ROUTINE を実装できます。 ドライバーを使用して、 [ **KeRegisterBugCheckReasonCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckcallback)と[ **KeDeregisterBugCheckReasonCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckcallback)ルーチンを登録するにはこれら 3 種類の*BugCheckXxxCallback*コールバック ルーチン。

[ *KBUGCHECK_CALLBACK_REASON 列挙*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_kbugcheck_callback_reason)バック ルーチンの呼び出しの種類を指定します。

次の種類のコールバックがよく使用されます。

**KbCallbackAddPages** - コールバックが提供するように実行されるか、システムがクラッシュの主要なセクションに追加するデータのより多くのページのダンプ ファイル。 [ *KBUGCHECK_ADD_PAGES 構造*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_add_pages) KbCallbackAddPages コールバック ルーチンによってクラッシュ ダンプ ファイルに書き込まれるドライバーが提供するデータの 1 つまたは複数のページについて説明します。 この種類のコールバックの詳細については、のこのトピックの「「を実装する KbCallbackAddPages コールバック日常的な」参照してください。

**KbCallbackDumpIo** -コールバックがダンプ ファイルのセクションが書き込まれるたびに実行します。 [KBUGCHECK_DUMP_IO 構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_dump_io)クラッシュ ダンプ ファイルで I/O 操作を記述するために使用します。 この種類のコールバックの詳細については、のこのトピックの「「を実装する KbCallbackDumpIo コールバック日常的な」参照してください。

**KbCallbackSecondaryDumpData** -コールバックがダンプ ファイルのセクションが書き込まれるたびに実行します。 [KBUGCHECK_SECONDARY_DUMP_DATA 構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_secondary_dump_data)構造がクラッシュ ダンプ ファイルに書き込まれるドライバーが提供するデータのセクションについて説明します。 この種類のコールバックの詳細については、のこのトピックの「「を実装する KbCallbackSecondaryDumpData コールバック日常的な」参照してください。

バグ チェックのデータの詳細については、次を参照してください。[バグ チェック コールバックのデータの読み取り](https://docs.microsoft.com/windows-hardware/drivers/debugger/reading-bug-check-callback-data)します。


## <a name="bug-check-callback-routine-restrictions"></a>バグ チェック コールバックの日常的な制限事項

IRQL でバグ チェック コールバック ルーチンが実行される高 =\_レベルで、何ができるに厳密な制限が課されます。

バグ チェック コールバック ルーチンことはできません。

- メモリの割り当て

- ページング可能なメモリのアクセス

- すべての同期機構を使用します。

- IRQL で実行する必要がある任意のルーチンを呼び出すディスパッチ =\_レベル以下

バグ チェック コールバック ルーチンのため同期は必要ありません、中断せずに実行することが保証されます。 (バグ チェック ルーチンが任意の同期機構を使用している場合、システム デッドロックが発生します。)

ドライバーのバグ チェック コールバック ルーチンが安全に使用できます、<strong>読み取り\_ポート\_*XXX</strong><em>、*読み取り\_登録\_</em>XXX <strong><em>、*</em>書き込み\_ポート\_* XXX</strong><em>、および**書き込み\_登録\_</em>XXX*** ドライバーのデバイスと通信するルーチン。 (これらのルーチンの詳細については、次を参照してください[ハードウェア アブストラクション レイヤー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff546644)。)。

## <a name="using-bugcheckcallback"></a>BugCheckCallback を使用します。

Windows XP Service Pack 1 (SP1) および Windows Server 2003 では、前にドライバーも使用できます BugCheckCallback クラッシュ ダンプ ファイルにデータを格納しますシステムがクラッシュ ダンプ ファイルがバッファーに書き込まれるため、データを書き込む前に各 BugCheckCallback ルーチンを呼び出す。渡される BugCheckCallback がクラッシュ ダンプ ファイルに保存されていました。

詳細については、次を参照してください。 [ *KBUGCHECK_CALLBACK_ROUTINE コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_callback_routine)します。


## <a name="implementing-kbcallbackaddpages-callback-routine"></a>KbCallbackAddPages コールバック ルーチンを実装します。

カーネル モード ドライバーを実装できる、 <i>KbCallbackAddPages</i>バグ チェックが発生した場合、クラッシュ ダンプ ファイルにデータの 1 つまたは複数のページを追加するコールバック ルーチン。 ドライバーの呼び出しに、オペレーティング システムをこのルーチンを登録する、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553110">KeRegisterBugCheckReasonCallback</a>ルーチン。 ドライバーをアンロードする前に呼び出す必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552003">KeDeregisterBugCheckReasonCallback</a>ルーチン登録を削除します。

登録済み Windows 8 以降で<i>KbCallbackAddPages</i>ルーチンは、中に呼び出される、<a href="https://msdn.microsoft.com/library/windows/hardware/ff551867">カーネル メモリ ダンプ</a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff539190">完全メモリ ダンプ</a>します。 以前のバージョンの Windows の登録済み<i>KbCallbackAddPages</i>ルーチンは、完全メモリ ダンプ中ではないが、カーネルのメモリ ダンプを作成中に呼び出されます。 既定では、カーネル メモリ ダンプには、使用されている Windows カーネルによってバグ チェックが発生した時点で完全メモリ ダンプには、すべての Windows で使用される物理メモリが含まれていますが、物理的なページのみが含まれています。 完全メモリ ダンプは、既定では、含まれません、プラットフォーム ファームウェアによって使用される物理メモリ。

<i>KbCallbackAddPages</i>ルーチンは、ダンプ ファイルに追加するドライバー固有のデータを指定できます。 たとえば、カーネル メモリ ダンプの場合、この追加のデータは、物理ページの仮想メモリ内のシステム アドレスの範囲にマップされるされませんが、ドライバーをデバッグするのに役立つ情報を含むを含めることができます。 <i>KbCallbackAddPages</i>ルーチン ダンプ ファイルに、ドライバーが所有している物理ページがマップされていないか、ユーザー モード仮想メモリ アドレスにマップされるとの追加の可能性があります。

オペレーティング システムを呼び出すすべてのバグ チェックが発生したときに、登録済み<i>KbCallbackAddPages</i>クラッシュ ダンプ ファイルに追加するデータ用のドライバーをポーリングするルーチン。 各呼び出しは、クラッシュ ダンプ ファイルに、連続したデータの 1 つまたは複数のページを追加します。 A <i>KbCallbackAddPages</i>ルーチンは、仮想アドレスまたは開始ページの物理アドレスのいずれかを指定できます。 複数のページは、呼び出し中に指定した場合、ページが開始アドレスが仮想か物理かどうかに応じて、仮想または物理メモリ内で連続しています。 連続しない複数のページを指定する、 <i>KbCallbackAddPages</i>ルーチンでフラグを設定できる、 <b>KBUGCHECK_ADD_PAGES</b>構造を示すことは、追加のデータ、もう一度呼び出す必要があります。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551839">KBUGCHECK_ADD_PAGES</a>します。

セカンダリのクラッシュ ダンプのリージョンにデータを追加、KbCallbackSecondaryDumpData ルーチンとは異なり、 <i>KbCallbackAddPages</i>ルーチンは、プライマリのクラッシュ ダンプのリージョンにデータのページを追加します。 デバッグ、プライマリのクラッシュ時にダンプ データはセカンダリのクラッシュ ダンプ データよりも簡単にアクセスします。

オペレーティング システムの呼び出しの前に、 <i>KbCallbackAddPages</i>塗りつぶす、日常的な<b>BugCheckCode</b>のメンバー、 <b>KBUGCHECK_ADD_PAGES</b>その構造体<i>ReasonSpecificData</i>を指します。 呼び出し中に、 <i>KbCallbackAddPages</i>ルーチンの値を設定する必要があります、<b>フラグ</b>、<b>アドレス</b>、および<b>カウント</b>this のメンバー構造体。 場合、 <i>KbCallbackAddPages</i>ルーチンには、1 つ以上の時間を呼び出すと、オペレーティング システムに、コールバック ルーチンを記述した値を保持する、<b>コンテキスト</b>前の呼び出しでのメンバー。 最初の呼び出しの前に、オペレーティング システムを初期化します<b>コンテキスト</b>に<b>NULL</b>します。

A <i>KbCallbackAddPages</i>ルーチンは非常に制限されてが実行できるアクションにします。 詳細については、このトピックの「バグ チェック コールバック日常的な制限事項」を参照してください。

## <a name="implementing-a-kbcallbackdumpio-callback-routine"></a>KbCallbackDumpIo コールバック ルーチンを実装します。

ドライバーの<i>KbCallbackDumpIo</i>コールバック ルーチンには、クラッシュ ダンプ ファイルにデータが書き込まれるたびには呼び出されます。 システムが成功、 <i>ReasonSpecificData</i>パラメーター、書き込まれるデータの説明。 <b>バッファー</b>メンバーが現在のデータを指す、 <b>BufferLength</b>メンバーがその長さを指定します。 <b>型</b>メンバーを現在作成中、ダンプ ファイルのヘッダー情報、メモリの状態、またはドライバーによって提供されるデータなどのデータの種類を示します。 情報の種類の説明は、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551871">KBUGCHECK_DUMP_IO_TYPE</a>します。

システムは、順番に、または正しくない順序、クラッシュ ダンプ ファイルを作成できます。 システム順番にクラッシュ ダンプ ファイルを書き込む場合、<b>オフセット</b>のメンバー <i>ReasonSpecificData</i>は-1 ですそうしないと、<b>オフセット</b>で現在のオフセットに設定されます。クラッシュ ダンプ ファイルのバイト数。

各呼び出し、システムでは、順番にファイルを書き込む、 <i>KbCallbackDumpIo</i>ルーチンのいずれかの回ヘッダー情報を記述する場合、または (<b>型</b> = <b>KbDumpIoHeader</b>)、ダンプ ファイルが、クラッシュのメインの本文を記述すると、1 つ以上の時間 (<b>型</b> = <b>KbDumpIoBody</b>)、1 つまたは複数回セカンダリ ダンプ データを書き込むときに(<b>型</b> = <b>KbDumpIoSecondaryDumpData</b>)。 コールバックを呼び出して、システムのクラッシュ ダンプ ファイルの書き込みが完了すると<b>バッファー</b> = <b>NULL</b>、 <b>BufferLength</b> = 0、および<b>型</b>  =  <b>KbDumpIoComplete</b>します。

主な目的、 <i>KbCallbackDumpIo</i>ルーチンは、システムのクラッシュ ダンプ データ ディスク以外のデバイスへの書き込みを許可します。 たとえば、システム状態を監視するデバイスは、システムのバグ チェックが発行されたことを報告して、分析、クラッシュ ダンプを提供するコールバックを使用できます。

使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553110">KeRegisterBugCheckReasonCallback</a>を登録する、 <i>KbCallbackDumpIo</i>ルーチン。 ドライバーを使用してコールバックを削除できる、その後、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552003">KeDeregisterBugCheckReasonCallback</a>ルーチン。 任意の登録済みのコールバックを削除する必要があります、ドライバーは、読み込まれたことができる場合、その<a href="https://msdn.microsoft.com/library/windows/hardware/ff564886">アンロード</a>ルーチン。

A <i>KbCallbackDumpIo</i>ルーチンがかかることがアクションで厳密に制限されています。 詳細については、このトピックの「バグ チェック コールバック日常的な制限事項」を参照してください。

## <a name="implementing-kbcallbacksecondarydumpdata"></a>KbCallbackSecondaryDumpData を実装します。

システムを使用して<i>KbCallbackSecondaryDumpData</i>クラッシュ用のドライバーをポーリングするルーチンがデータをダンプします。

システムのセット、 <b>InBuffer</b>、 <b>InBufferLength</b>、 <b>OutBuffer</b>、および<b>MaximumAllowed</b>のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551879">KBUGCHECK_SECONDARY_DUMP_DATA</a>構造体<i>ReasonSpecificData</i>を指します。 <b>MaximumAllowed</b>メンバーの最大データ量を指定ダンプ ルーチンを提供できます。

値、 <b>OutBuffer</b>メンバーが、サイズのドライバーのダンプ データ、またはデータ自体には、次のように、システムが要求するかどうかを判断します。

<ul>
<li>
場合、 <b>OutBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA のメンバーが<b>NULL</b>システムがサイズ情報を要求するだけです。 <i>KbCallbackSecondaryDumpData</i>ルーチンを入力、 <b>OutBuffer</b>と<b>OutBufferLength</b>メンバー。 
</li>

<li>
場合、 <b>OutBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA equals のメンバー、 <b>InBuffer</b>メンバー、システムは、ドライバーのセカンダリ ダンプ データを要求しています。 <i>KbCallbackSecondaryDumpData</i>ルーチンを入力、 <b>OutBuffer</b>と<b>OutBufferLength</b>メンバー、およびによって指定されたバッファーにデータを書き込みます<b>OutBuffer</b>します。
</li>
</ul>

<b>InBuffer</b>ルーチンの使用するための小さなバッファーを指す KBUGCHECK_SECONDARY_DUMP_DATA のメンバー。 <b>InBufferLength</b>メンバーが、バッファーのサイズを指定します。 書き込まれるデータの量がある場合より小さい<b>InBufferLength</b>、コールバック ルーチンでは、このバッファーを使用して、システムにクラッシュ ダンプ データを提供することができます。 コールバック ルーチンを設定し、 <b>OutBuffer</b>に<b>InBuffer</b>と<b>OutBufferLength</b>バッファーに書き込まれたデータ量が実際にします。

超えるデータ量を記述する必要のあるドライバー <b>InBufferLength</b>独自のバッファーを使用して、データを提供することができます。 このバッファーは、前に、コールバック ルーチンが実行され (非ページ プール) などのメモリ内に存在する必要がありますに割り当てられている必要があります。 コールバック ルーチンを設定し、 <b>OutBuffer</b> 、ドライバーのバッファーを指すと<b>OutBufferLength</b>クラッシュ ダンプ ファイルに書き込まれるバッファー内のデータの量にします。

Windows XP および Windows Server 2003 では場合、 <b>OutBuffer</b>はドライバーによって割り当てられたバッファーを指すように設定、バッファーはメモリ内のページに配置の境界で開始する必要があります。 それ以外の場合、クラッシュ ダンプ ファイルのセカンダリのデータ領域にデータは書き込まれません。 Windows Vista および Windows の以降のバージョンでは、このようなアラインメント要件はありません。

クラッシュ ダンプ ファイルに書き込まれるデータの各ブロックがの値でタグ付け、 <b>Guid</b>のメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/ff551879">KBUGCHECK_SECONDARY_DUMP_DATA</a>します。 使用される GUID は、ドライバーに一意である必要があります。 この GUID に対応するセカンダリ ダンプ データを表示するには、使用することができます、 <b>.enumtag</b>コマンドまたは<b>IDebugDataSpaces3::ReadTagged</b>デバッガー拡張メソッド。 デバッガーとデバッガー拡張機能については、次を参照してください。 <a href="https://msdn.microsoft.com/938ef180-84de-442f-9b6c-1138c2fc8d5a">Windows デバッグ</a>します。

ドライバーは、クラッシュ ダンプ ファイルに同じ GUID を持つ複数のブロックを書き込むことができますが、これは非常に低い実際には、最初のブロックのみがデバッガーにアクセスできるためです。 複数の登録ドライバー <i>KbCallbackSecondaryDumpData</i>ルーチンは、各コールバックの一意の GUID を割り当てる必要があります。

使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553110">KeRegisterBugCheckReasonCallback</a>を登録する、 <i>KbCallbackSecondaryDumpData</i>ルーチン。 ドライバーを使用して、コールバック ルーチンを削除できます、その後、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552003">KeDeregisterBugCheckReasonCallback</a>ルーチン。 ドライバーをアンロード、できるかどうかは、登録されたコールバック ルーチンを削除する必要があります、<a href="https://msdn.microsoft.com/library/windows/hardware/ff564886">アンロード</a>ルーチン。

A <i>KbCallbackSecondaryDumpData</i>ルーチンは非常に制限されてが実行できるアクションにします。 詳細については、このトピックの「バグ チェック コールバック日常的な制限事項」を参照してください。


#### <a name="callback-routine-examples"></a>コールバック ルーチンの例

コールバック ルーチンを定義するには、関数の宣言を定義するコールバック ルーチンの種類を識別するまず提供する必要があります。 Windows では、ドライバーの一連のコールバック関数の型を提供します。 コールバック関数を使用して関数を宣言することを型<a href="https://msdn.microsoft.com/2F3549EF-B50F-455A-BDC7-1F67782B8DCA">Code Analysis for Drivers</a>、 <a href="https://msdn.microsoft.com/74feeb16-387c-4796-987a-aff3fb79b556">Static Driver Verifier</a> (SDV)、その他の検証ツールは、エラーを検索して、書き込みが必要ですWindows オペレーティング システムのドライバーです。

たとえば、定義するため、 <i>KbCallbackAddPages</i>というコールバック ルーチン<code>MyKbCallbackAddPages</code>KBUGCHECK_REASON_CALLBACK_ROUTINE 型を使用して、このコード例で示すように。

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>KBUGCHECK_REASON_CALLBACK_ROUTINE MyBugCheckAddPagesCallback;</pre>
</td>
</tr>
</table></span></div>
次に、としては、次のように、コールバック ルーチンを実装します。

<div class="code"><span codelanguage=""><table>
<tr>
<th></th>
</tr>
<tr>
<td>
<pre>_Use_decl_annotations_
VOID
  MyBugCheckAddPagesCallback(
    KBUGCHECK_CALLBACK_REASON  Reason,
    struct _KBUGCHECK_REASON_CALLBACK_RECORD  *Record,
    PVOID  ReasonSpecificData,
    ULONG  ReasonSpecificDataLength 
    )
  {
      // Function body
  }</pre>
</td>
</tr>
</table></span></div>
KBUGCHECK_REASON_CALLBACK_ROUTINE 関数の型は、Wdm.h のヘッダー ファイルで定義されます。 コード分析ツールを実行すると、エラーをより正確に特定、追加することを確認する、 _Use_decl_annotations_関数定義に注釈。 _Use_decl_annotations_注釈により、ヘッダー ファイルで KBUGCHECK_REASON_CALLBACK_ROUTINE 関数の型に適用される注釈を使用するようになります。 関数宣言子の要件の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/3260b53e-82be-4dbc-8ac5-d0e52de77f9d">を使用して関数の役割の種類 WDM ドライバーで関数を宣言する</a>します。 について_Use_decl_annotations_を参照してください<a href="https://go.microsoft.com/fwlink/p/?linkid=286697">関数の動作に注釈を付ける</a>します。

<div class="code"></div>


