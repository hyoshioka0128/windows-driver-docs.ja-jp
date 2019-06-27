---
title: バグ チェックのためのコールバック ルーチンを記述します。
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
ms.openlocfilehash: b19f4e48fddc4f9550290dedd3776feb422c77f7
ms.sourcegitcommit: 95e3fd15d9c00a341e774d58a927856d750a35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410010"
---
# <a name="writing-a-bug-check-reason-callback-routine"></a>バグ チェックのためのコールバック ルーチンを記述します。

ドライバーが必要に応じて指定できます、 [ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)クラッシュ ダンプの後、システムが呼び出すコールバック関数は、ファイルが書き込まれます。

> [!NOTE]
> この記事では、バグのチェックをについて説明します*理由*コールバック ルーチン、および not、 [ *KBUGCHECK_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_callback_routine)コールバック関数。

このコールバックで、ドライバーでは次のことができます。

* ドライバー固有のデータをクラッシュ ダンプ ファイルに追加します。
* デバイスを既知の状態をリセットします。

登録およびコールバックを削除するには、次のルーチンを使用します。

* [**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)
* [**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)

基づく動作を変更すると、このコールバックの型がオーバー ロードされた、 [ **KBUGCHECK_CALLBACK_REASON** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_kbugcheck_callback_reason)登録時に指定された定数値。  この記事では、さまざまな使用シナリオについて説明します。

バグ チェックのデータの詳細については、次を参照してください。[バグ チェック コールバックのデータの読み取り](https://docs.microsoft.com/windows-hardware/drivers/debugger/reading-bug-check-callback-data)します。

## <a name="bug-check-callback-routine-restrictions"></a>バグ チェック コールバックの日常的な制限事項

IRQL でバグ チェック コールバック ルーチンが実行される高 =\_レベルで、何ができるに厳密な制限が課されます。

バグ チェック コールバック ルーチンことはできません。

* メモリの割り当て
* ページング可能なメモリのアクセス
* すべての同期機構を使用します。
* IRQL で実行する必要がある任意のルーチンを呼び出すディスパッチ =\_レベル以下

バグ チェック コールバック ルーチンのため同期は必要ありません、中断せずに実行することが保証されます。 (バグ チェック ルーチンが任意の同期機構を使用している場合、システム デッドロックが発生します。)

ドライバーのバグ チェック コールバック ルーチンが安全に使用できます、**読み取り\_ポート\_<em>XXX</em>** 、**読み取り\_登録\_<em>XXX</em>** 、**書き込み\_ポート\_<em>XXX</em>** 、および**書き込み\_レジスタ\_ <em>XXX</em>** ドライバーのデバイスと通信するルーチン。 (これらのルーチンの詳細については、次を参照してください[ハードウェア アブストラクション レイヤー ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。)。

## <a name="implementing-a-kbcallbackaddpages-callback-routine"></a>KbCallbackAddPages コールバック ルーチンを実装します。

カーネル モード ドライバーを実装できる、 [ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)型のコールバック関数<i>KbCallbackAddPages</i>がクラッシュするデータの 1 つまたは複数のページを追加するにはバグ チェックが発生した場合にファイルをダンプします。 ドライバーの呼び出しに、オペレーティング システムをこのルーチンを登録する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a>ルーチン。 ドライバーをアンロードする前に呼び出す必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a>ルーチン登録を削除します。

登録済み Windows 8 以降で<i>KbCallbackAddPages</i>ルーチンは、中に呼び出される、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-memory-dump">カーネル メモリ ダンプ</a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/complete-memory-dump">完全メモリ ダンプ</a>します。 以前のバージョンの Windows の登録済み<i>KbCallbackAddPages</i>ルーチンは、完全メモリ ダンプ中ではないが、カーネルのメモリ ダンプを作成中に呼び出されます。 既定では、カーネル メモリ ダンプには、使用されている Windows カーネルによってバグ チェックが発生した時点で完全メモリ ダンプには、すべての Windows で使用される物理メモリが含まれていますが、物理的なページのみが含まれています。 完全メモリ ダンプは、既定では、含まれません、プラットフォーム ファームウェアによって使用される物理メモリ。

<i>KbCallbackAddPages</i>ルーチンは、ダンプ ファイルに追加するドライバー固有のデータを指定できます。 たとえば、カーネル メモリ ダンプの場合、この追加のデータは、物理ページの仮想メモリ内のシステム アドレスの範囲にマップされるされませんが、ドライバーをデバッグするのに役立つ情報を含むを含めることができます。 <i>KbCallbackAddPages</i>ルーチン ダンプ ファイルに、ドライバーが所有している物理ページがマップされていないか、ユーザー モード仮想メモリ アドレスにマップされるとの追加の可能性があります。

オペレーティング システムを呼び出すすべてのバグ チェックが発生したときに、登録済み<i>KbCallbackAddPages</i>クラッシュ ダンプ ファイルに追加するデータ用のドライバーをポーリングするルーチン。 各呼び出しは、クラッシュ ダンプ ファイルに、連続したデータの 1 つまたは複数のページを追加します。 A <i>KbCallbackAddPages</i>ルーチンは、仮想アドレスまたは開始ページの物理アドレスのいずれかを指定できます。 複数のページは、呼び出し中に指定した場合、ページが開始アドレスが仮想か物理かどうかに応じて、仮想または物理メモリ内で連続しています。 連続しない複数のページを指定する、 <i>KbCallbackAddPages</i>ルーチンでフラグを設定できる、 <b>KBUGCHECK_ADD_PAGES</b>構造を示すことは、追加のデータ、もう一度呼び出す必要があります。 詳細については、次を参照してください。、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_add_pages">KBUGCHECK_ADD_PAGES</a>構造体。

セカンダリのクラッシュ ダンプのリージョンにデータを追加、KbCallbackSecondaryDumpData ルーチンとは異なり、 <i>KbCallbackAddPages</i>ルーチンは、プライマリのクラッシュ ダンプのリージョンにデータのページを追加します。 デバッグ、プライマリのクラッシュ時にダンプ データはセカンダリのクラッシュ ダンプ データよりも簡単にアクセスします。

オペレーティング システムの呼び出しの前に、 <i>KbCallbackAddPages</i>塗りつぶす、日常的な<b>BugCheckCode</b>のメンバー、 <b>KBUGCHECK_ADD_PAGES</b>その構造体<i>ReasonSpecificData</i>を指します。 呼び出し中に、 <i>KbCallbackAddPages</i>ルーチンの値を設定する必要があります、<b>フラグ</b>、<b>アドレス</b>、および<b>カウント</b>this のメンバー構造体。 場合、 <i>KbCallbackAddPages</i>ルーチンには、1 つ以上の時間を呼び出すと、オペレーティング システムに、コールバック ルーチンを記述した値を保持する、<b>コンテキスト</b>前の呼び出しでのメンバー。 最初の呼び出しの前に、オペレーティング システムを初期化します<b>コンテキスト</b>に<b>NULL</b>します。

A <i>KbCallbackAddPages</i>ルーチンは非常に制限されてが実行できるアクションにします。 詳細については、このトピックの「バグ チェック コールバック日常的な制限事項」を参照してください。

## <a name="implementing-a-kbcallbackdumpio-callback-routine"></a>KbCallbackDumpIo コールバック ルーチンを実装します。

カーネル モード ドライバーを実装できる、 [ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)型のコールバック関数<i>KbCallbackDumpIo</i>に各時刻のデータが書き込まれる作業を実行するにはクラッシュ ダンプ ファイル。 システムが成功、 <i>ReasonSpecificData</i>パラメーター、書き込まれるデータの説明。 <b>バッファー</b>メンバーが現在のデータを指す、 <b>BufferLength</b>メンバーがその長さを指定します。 <b>型</b>メンバーを現在作成中、ダンプ ファイルのヘッダー情報、メモリの状態、またはドライバーによって提供されるデータなどのデータの種類を示します。 情報の種類の説明は、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_kbugcheck_dump_io_type">KBUGCHECK_DUMP_IO_TYPE</a>します。

システムは、順番に、または正しくない順序、クラッシュ ダンプ ファイルを作成できます。 システム順番にクラッシュ ダンプ ファイルを書き込む場合、<b>オフセット</b>のメンバー <i>ReasonSpecificData</i>は-1 ですそうしないと、<b>オフセット</b>で現在のオフセットに設定されます。クラッシュ ダンプ ファイルのバイト数。

各呼び出し、システムでは、順番にファイルを書き込む、 <i>KbCallbackDumpIo</i>ルーチンのいずれかの回ヘッダー情報を記述する場合、または (<b>型</b> = <b>KbDumpIoHeader</b>)、ダンプ ファイルが、クラッシュのメインの本文を記述すると、1 つ以上の時間 (<b>型</b> = <b>KbDumpIoBody</b>)、1 つまたは複数回セカンダリ ダンプ データを書き込むときに(<b>型</b> = <b>KbDumpIoSecondaryDumpData</b>)。 コールバックを呼び出して、システムのクラッシュ ダンプ ファイルの書き込みが完了すると<b>バッファー</b> = <b>NULL</b>、 <b>BufferLength</b> = 0、および<b>型</b>  =  <b>KbDumpIoComplete</b>します。

主な目的、 <i>KbCallbackDumpIo</i>ルーチンは、システムのクラッシュ ダンプ データ ディスク以外のデバイスへの書き込みを許可します。 たとえば、システム状態を監視するデバイスは、システムのバグ チェックが発行されたことを報告して、分析、クラッシュ ダンプを提供するコールバックを使用できます。

使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a>を登録する、 <i>KbCallbackDumpIo</i>ルーチン。 ドライバーを使用してコールバックを削除できる、その後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a>ルーチン。 任意の登録済みのコールバックを削除する必要があります、ドライバーは、読み込まれたことができる場合、その<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload">アンロード</a>ルーチン。

A <i>KbCallbackDumpIo</i>ルーチンがかかることがアクションで厳密に制限されています。 詳細については、このトピックの「バグ チェック コールバック日常的な制限事項」を参照してください。

## <a name="implementing-a-kbcallbacksecondarydumpdata-routine"></a>KbCallbackSecondaryDumpData ルーチンを実装します。

カーネル モード ドライバーを実装できる、 [ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)型のコールバック関数<i>KbCallbackSecondaryDumpData</i>に追加するデータを提供するにはクラッシュ ダンプ ファイル。

システムのセット、 <b>InBuffer</b>、 <b>InBufferLength</b>、 <b>OutBuffer</b>、および<b>MaximumAllowed</b>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a>構造体<i>ReasonSpecificData</i>を指します。 <b>MaximumAllowed</b>メンバーの最大データ量を指定ダンプ ルーチンを提供できます。

値、 <b>OutBuffer</b>メンバーが、サイズのドライバーのダンプ データ、またはデータ自体には、次のように、システムが要求するかどうかを判断します。

* 場合、 <b>OutBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA のメンバーが<b>NULL</b>システムがサイズ情報を要求するだけです。 <i>KbCallbackSecondaryDumpData</i>ルーチンを入力、 <b>OutBuffer</b>と<b>OutBufferLength</b>メンバー。 
* 場合、 <b>OutBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA equals のメンバー、 <b>InBuffer</b>メンバー、システムは、ドライバーのセカンダリ ダンプ データを要求しています。 <i>KbCallbackSecondaryDumpData</i>ルーチンを入力、 <b>OutBuffer</b>と<b>OutBufferLength</b>メンバー、およびによって指定されたバッファーにデータを書き込みます<b>OutBuffer</b>します。

<b>InBuffer</b>ルーチンの使用するための小さなバッファーを指す KBUGCHECK_SECONDARY_DUMP_DATA のメンバー。 <b>InBufferLength</b>メンバーが、バッファーのサイズを指定します。 書き込まれるデータの量がある場合より小さい<b>InBufferLength</b>、コールバック ルーチンでは、このバッファーを使用して、システムにクラッシュ ダンプ データを提供することができます。 コールバック ルーチンを設定し、 <b>OutBuffer</b>に<b>InBuffer</b>と<b>OutBufferLength</b>バッファーに書き込まれたデータ量が実際にします。

超えるデータ量を記述する必要のあるドライバー <b>InBufferLength</b>独自のバッファーを使用して、データを提供することができます。 このバッファーは、前に、コールバック ルーチンが実行され (非ページ プール) などのメモリ内に存在する必要がありますに割り当てられている必要があります。 コールバック ルーチンを設定し、 <b>OutBuffer</b> 、ドライバーのバッファーを指すと<b>OutBufferLength</b>クラッシュ ダンプ ファイルに書き込まれるバッファー内のデータの量にします。

クラッシュ ダンプ ファイルに書き込まれるデータの各ブロックがの値でタグ付け、 <b>Guid</b>のメンバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a>します。 使用される GUID は、ドライバーに一意である必要があります。 この GUID に対応するセカンダリ ダンプ データを表示するには、使用することができます、 <b>.enumtag</b>コマンドまたは<b>IDebugDataSpaces3::ReadTagged</b>デバッガー拡張メソッド。 デバッガーとデバッガー拡張機能については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/index">Windows デバッグ</a>します。

ドライバーは、クラッシュ ダンプ ファイルに同じ GUID を持つ複数のブロックを書き込むことができますが、これは非常に低い実際には、最初のブロックのみがデバッガーにアクセスできるためです。 複数の登録ドライバー <i>KbCallbackSecondaryDumpData</i>ルーチンは、各コールバックの一意の GUID を割り当てる必要があります。

使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a>を登録する、 <i>KbCallbackSecondaryDumpData</i>ルーチン。 ドライバーを使用して、コールバック ルーチンを削除できます、その後、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a>ルーチン。 ドライバーをアンロード、できるかどうかは、登録されたコールバック ルーチンを削除する必要があります、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload">アンロード</a>ルーチン。

A <i>KbCallbackSecondaryDumpData</i>ルーチンは非常に制限されてが実行できるアクションにします。 詳細については、このトピックの「バグ チェック コールバック日常的な制限事項」を参照してください。

## <a name="implementing-a-kbcallbacktriagedumpdata-routine"></a>KbCallbackTriageDumpData ルーチンを実装します。

Windows 10、バージョンは 1809 および Windows Server 2019 以降、カーネル モード ドライバーを実装できます、 [ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)型のコールバック関数*KbCallbackTriageDumpData*仮想メモリの範囲を分割したミニダンプ ファイルに追加します。  ダンプのデータが記載されて、 [ **KBUGCHECK_TRIAGE_DUMP_DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_triage_dump_data)構造体。

次の例では、ドライバーは、トリアージ ダンプのアレイを構成し、コールバックの最小限の実装を登録し。

```cpp
// Globals 
 
KBUGCHECK_REASON_CALLBACK_RECORD ExampleBugcheckCallbackRecord; 
PKTRIAGE_DUMP_DATA_ARRAY gTriageDumpDataArray; 
 
//  call this register function from DriverInit, etc.
 
VOID ExampleRegisterTriageDataCallbacks() 
{ 
 
    // 
    // Allocate a triage dump array in the non-paged pool. 
    // 
 
gTriageDumpDataArray = 
    (PKTRIAGE_DUMP_DATA_ARRAY)ExAllocatePoolWithTag(NonPagedPoolNx, 2*PAGE_SIZE, "Xmpl"); 
 
    // 
    // Initialize the dump data block array. 
    // 
 
    KeInitializeTriageDumpDataArray( gTriageDumpDataArray, 2*PAGE_SIZE, "Example"); 
 
    KeInitializeCallbackRecord( &ExampleBugcheckCallbackRecord ); 
 
    KeRegisterBugCheckReasonCallback( 
        &ExampleBugCheckCallbackRecord, 
        ExampleBugCheckCallbackRoutine, 
        KbCallbackTriageDumpData, 
        "Example" 
        ); 
} 
 
// Callback function 
 
VOID 
ExampleBugCheckCallbackRoutine( 
    KBUGCHECK_CALLBACK_REASON Reason, 
    PKBUGCHECK_REASON_CALLBACK_RECORD Record, 
    PVOID Data, 
    ULONG Length 
    ) 
{ 
    PKBUGCHECK_TRIAGE_DUMP_DATA DumpData; 
    NTSTATUS Status; 
 
    DumpData = (PKBUGCHECK_TRIAGE_DUMP_DATA) Data; 
 
    Status = KeAddTriageDumpDataBlock(gTriageDumpDataArray, gImportant, SizeofGImportant); 
 
    // Pass our arrays back 
 
    if (NT_SUCCESS(Status)) { 
        DumpData->RequiredDataArray = gTriageDumpDataArray; 
    } 
 
    return; 
}
```


