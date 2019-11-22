---
title: バグ チェック理由コールバック ルーチンの記述
description: バグ チェック コールバック ルーチンの記述
ms.assetid: 62aefe67-e197-4c45-b994-19bd7369dbc1
keywords:
- バグチェックコールバックルーチン WDK カーネル
- コールバックルーチン WDK バグチェック
- 登録 (コールバックルーチンを)
- KeRegisterBugCheckCallback
- バグチェックコールバック
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: b58ddf3c0f032a22f9ce8784d8df44b7795c3e5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838300"
---
# <a name="writing-a-bug-check-reason-callback-routine"></a>バグ チェック理由コールバック ルーチンの記述

ドライバーは、必要に応じて、クラッシュダンプファイルが書き込まれた後にシステムが呼び出す[*KBUGCHECK_REASON_CALLBACK_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)コールバック関数を提供できます。

> [!NOTE]
> この記事では、 [*KBUGCHECK_CALLBACK_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_callback_routine)コールバック関数ではなく、バグチェックの*理由*コールバックルーチンについて説明します。

このコールバックでは、ドライバーは次のことを実行できます。

* ドライバー固有のデータをクラッシュダンプファイルに追加する
* デバイスを既知の状態にリセットする

コールバックを登録および削除するには、次のルーチンを使用します。

* [**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)
* [**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)

このコールバック型はオーバーロードされ、登録時に指定された[**KBUGCHECK_CALLBACK_REASON**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_kbugcheck_callback_reason)定数値に基づいて動作が変わります。  この記事では、さまざまな使用シナリオについて説明します。

バグチェックのデータに関する一般的な情報については、「[バグチェックのコールバックデータの読み取り](https://docs.microsoft.com/windows-hardware/drivers/debugger/reading-bug-check-callback-data)」を参照してください。

## <a name="bug-check-callback-routine-restrictions"></a>バグチェックコールバックルーチンの制限

バグチェックコールバックルーチンは、IRQL = HIGH\_レベルで実行されます。これにより、実行できる処理に強い制限が課されます。

バグチェックのコールバックルーチンには、次のことはできません。

* メモリの割り当て
* ページング可能メモリにアクセスする
* 任意の同期メカニズムを使用する
* IRQL = ディスパッチ\_レベル以下で実行する必要がある任意のルーチンを呼び出します。

バグチェックコールバックルーチンは中断せずに実行されることが保証されているため、同期は必要ありません。 (バグチェックルーチンで同期メカニズムが使用されている場合、システムはデッドロック状態になります)。

ドライバーのバグチェックコールバックルーチンでは、**読み取り\_ポート\_<em>xxx</em>** 、**読み取り\_登録\_<em>xxx</em>** 、 **\_ポート\_<em>xxx</em>の書き込み**、ドライバーのデバイスと通信するため\_ **<em>xxx</em>** ルーチンの登録を書き込むことができます。\_ (これらのルーチンの詳細については、「 [Hardware アブストラクションレイヤールーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))」を参照してください)。

## <a name="implementing-a-kbcallbackaddpages-callback-routine"></a>Kbcallback Addpages コールバックルーチンの実装

カーネルモードドライバーは、種類が<i>kbcallback Addpages</i>の[*KBUGCHECK_REASON_CALLBACK_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)コールバック関数を実装して、バグチェックが発生したときに1つ以上のデータページをクラッシュダンプファイルに追加できます。 このルーチンをオペレーティングシステムに登録するために、ドライバーは<b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a></b>ルーチンを呼び出します。 ドライバーがアンロードされる前に、 <b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a></b>ルーチンを呼び出して登録を削除する必要があります。

Windows 8 以降では、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-memory-dump">カーネルメモリダンプ</a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/complete-memory-dump">完全なメモリダンプ</a>中に、登録されている<i>kbの addpages</i>ルーチンが呼び出されます。 以前のバージョンの Windows では、登録されている<i>Kbの Addpages</i>ルーチンは、カーネルメモリダンプ中に呼び出されますが、完全なメモリダンプでは呼び出されません。 既定では、カーネルメモリダンプには、バグチェックが発生した時点で Windows カーネルによって使用されている物理ページのみが含まれます。一方、完全なメモリダンプには、Windows によって使用されているすべての物理メモリが含まれます。 既定では、完全なメモリダンプには、プラットフォームファームウェアによって使用される物理メモリが含まれません。

<i>Kbcallbackaddpages</i>ルーチンは、ダンプファイルに追加するドライバー固有のデータを提供できます。 たとえば、カーネルメモリダンプの場合、この追加データには、仮想メモリ内のシステムアドレス範囲にマップされていないが、ドライバーのデバッグに役立つ情報が含まれている物理ページを含めることができます。 <i>Kbて Addpages</i>ルーチンは、マップされていないか、仮想メモリ内のユーザーモードアドレスにマップされているドライバー所有の物理ページをダンプファイルに追加することがあります。

バグチェックが発生すると、オペレーティングシステムは登録されているすべての<i>Kbcallbackaddpages</i>ルーチンを呼び出して、データのドライバーをポーリングし、クラッシュダンプファイルに追加します。 各呼び出しでは、連続したデータの1つ以上のページがクラッシュダンプファイルに追加されます。 <i>Kb/Addpages</i>ルーチンでは、開始ページの仮想アドレスまたは物理アドレスを指定できます。 1回の呼び出しで複数のページが指定されている場合は、開始アドレスが仮想か物理かによって、仮想メモリまたは物理メモリの各ページが連続しています。 連続していないページを指定するために、 <i>Kbの Addpages</i>ルーチンは、追加のデータが含まれていて、再度呼び出す必要があることを示すフラグを<b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_add_pages">KBUGCHECK_ADD_PAGES</a></b>構造に設定できます。

セカンダリクラッシュダンプ領域にデータを追加する*Kb/Secondarydumpdata*ルーチンとは異なり、 <i>Kbkbaddpages</i>ルーチンは、データのページをプライマリクラッシュダンプ領域に追加します。 デバッグ中、プライマリクラッシュダンプデータは、セカンダリクラッシュダンプデータよりも簡単にアクセスできます。

オペレーティングシステムは、指定されたデータポイントを<i>理由</i>として、 <b>KBUGCHECK_ADD_PAGES</b>構造体の<b>バグ checkcode</b>メンバーを入力します。 <i>Kb/Addpages</i>ルーチンでは、この構造体の<b>Flags</b>、 <b>Address</b>、 <b>Count</b>の各メンバーの値を設定する必要があります。

オペレーティングシステムは、 <i>kbて Addpages</i>を初めて呼び出す前に、<b>コンテキスト</b>を<b>NULL</b>に初期化します。 <i>Kbcallback Addpages</i>ルーチンが2回以上呼び出された場合、オペレーティングシステムは、コールバックルーチンが前回の呼び出しで<b>コンテキスト</b>メンバーに書き込んだ値を保持します。

<i>Kb/Addpages</i>ルーチンは、実行できるアクションで非常に制限されています。 詳細については、「[バグチェックのコールバックルーチンの制限](#bug-check-callback-routine-restrictions)」を参照してください。

## <a name="implementing-a-kbcallbackdumpio-callback-routine"></a>KbCallbackDumpIo Callback ルーチンの実装

カーネルモードドライバーは、データがクラッシュダンプファイルに書き込まれるたびに処理を実行するために、 <i>KbCallbackDumpIo</i>型の[*KBUGCHECK_REASON_CALLBACK_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)コールバック関数を実装できます。 システムは、 [**KBUGCHECK_DUMP_IO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_dump_io)構造体へのポインターである、指定された<i>データ</i>パラメーターでを渡します。 <b>バッファー</b>メンバーは現在のデータを指し、 <b>bufferlength</b>メンバーはその長さを指定します。 <b>型</b>のメンバーは、ダンプファイルのヘッダー情報、メモリの状態、ドライバーによって提供されるデータなど、現在書き込まれているデータの種類を示します。 使用できる情報の種類の詳細については、「 <b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_kbugcheck_dump_io_type">KBUGCHECK_DUMP_IO_TYPE</a></b>列挙型」を参照してください。

システムは、クラッシュダンプファイルを順番に、または順番どおりに書き込むことができます。 システムがクラッシュダンプファイルを順番に書き込んでいる場合は、その<i>データ</i>の<b>オフセット</b>メンバーが-1 になります。それ以外の場合、<b>オフセット</b>は、クラッシュダンプファイル内の現在のオフセット (バイト単位) に設定されます。

システムがファイルを連続して書き込むと、各<i>KbCallbackDumpIo</i>ルーチンは、ヘッダー情報 (<b>型</b> = <b>KbDumpIoHeader</b>) を書き込むときに1回以上、クラッシュダンプのメインボディを書き込むときに1回以上呼び出されます。ファイル (<b>型</b> = <b>KbDumpIoBody</b>)、およびセカンダリダンプデータを書き込むときに1回以上 (<b>type</b> = <b>KbDumpIoSecondaryDumpData</b>)。 システムは、クラッシュダンプファイルの書き込みを完了すると、 <b>Buffer</b> = <b>NULL</b>、 <b>Bufferlength</b> = 0、および<b>Type</b> = <b>KbDumpIoComplete</b>を使用してコールバックを呼び出します。

<i>KbCallbackDumpIo</i>ルーチンの主な目的は、ディスク以外のデバイスにシステムクラッシュダンプデータを書き込むことができるようにすることです。 たとえば、システム状態を監視するデバイスは、コールバックを使用して、システムがバグチェックを発行したことを報告し、分析用のクラッシュダンプを提供できます。

<b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a></b>を使用して<i>KbCallbackDumpIo</i>ルーチンを登録します。 ドライバーは、その後、 <b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a></b>ルーチンを使用してコールバックを削除できます。 ドライバーをアンロードできる場合は、その<i><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload">DRIVER_UNLOAD</a></i>コールバック関数で登録されているコールバックを削除する必要があります。

<i>KbCallbackDumpIo</i>ルーチンは、実行できるアクションに厳密に制限されています。 詳細については、「[バグチェックのコールバックルーチンの制限](#bug-check-callback-routine-restrictions)」を参照してください。

## <a name="implementing-a-kbcallbacksecondarydumpdata-callback-routine"></a>Kbcallback Secondarydumpdata コールバックルーチンの実装

カーネルモードドライバーは、 <i>kbcallback Secondarydumpdata</i>型の[*KBUGCHECK_REASON_CALLBACK_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)コールバック関数を実装して、クラッシュダンプファイルに追加するデータを提供できます。

システムは、指定された<i>データ</i>が指す<b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a></b>構造体の<b>inbuffer</b>、 <b>inbufferlength</b>、 <b>outbuffer</b>、および<b>maximumallowed</b>のメンバーを設定します。 <b>Maximumallowed</b>メンバーは、ルーチンが提供できるダンプデータの最大量を指定します。

<b>Outbuffer</b>メンバーの値は、次のように、システムがドライバーのダンプデータのサイズを要求しているか、データ自体を要求しているかを判断します。

* KBUGCHECK_SECONDARY_DUMP_DATA の<b>Outbuffer</b>メンバーが<b>NULL</b>の場合、システムはサイズ情報のみを要求します。 <i>Kbの Secondarydumpdata</i>ルーチンは、 <b>Outbuffer</b>と<b>outbufferlength</b>のメンバーに入力します。 
* KBUGCHECK_SECONDARY_DUMP_DATA の<b>Outbuffer</b>メンバーが<b>inbuffer</b>メンバーと等しい場合、システムはドライバーのセカンダリダンプデータを要求しています。 <i>Kbて Secondarydumpdata</i>ルーチンは、 <b>Outbuffer</b>と<b>outbufferlength</b>のメンバーを設定し、 <b>outbuffer</b>によって指定されたバッファーにデータを書き込みます。

KBUGCHECK_SECONDARY_DUMP_DATA の<b>Inbuffer</b>メンバーは、ルーチンが使用するための小さなバッファーを指しています。 <b>Inbufferlength</b>メンバーは、バッファーのサイズを指定します。 書き込まれるデータの量が<b>Inbufferlength</b>より小さい場合、コールバックルーチンはこのバッファーを使用してクラッシュダンプデータをシステムに提供できます。 次に、コールバックルーチンは、 <b>outbuffer</b>を<b>Inbuffer</b>に、 <b>outbufferlength</b>をバッファーに書き込まれる実際のデータ量に設定します。

<b>Inbufferlength</b>より大きいデータを書き込む必要があるドライバーは、独自のバッファーを使用してデータを提供できます。 このバッファーは、コールバックルーチンが実行される前に割り当てられている必要があり、常駐メモリ (非ページプールなど) に存在する必要があります。 次に、コールバックルーチンは、ドライバーのバッファーを指すように<b>Outbuffer</b>を設定します。また、バッファー内のデータの量を<b>outbufferlength</b>に設定して、クラッシュダンプファイルに書き込みます。

クラッシュダンプファイルに書き込まれるデータの各ブロックには、 <b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a></b>構造体の<b>Guid</b>メンバーの値がタグ付けされます。 使用する GUID は、ドライバーに対して一意である必要があります。 この GUID に対応するセカンダリダンプデータを表示するには、デバッガー拡張機能で<b>enumtag</b>コマンドまたは<b>IDebugDataSpaces3:: readtagged</b>メソッドを使用します。 デバッガーとデバッガー拡張機能の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/index">Windows デバッグ</a>」を参照してください。

ドライバーは、同じ GUID を持つ複数のブロックをクラッシュダンプファイルに書き込むことができますが、デバッガーにアクセスできるのは最初のブロックだけなので、この方法は非常に悪くなります。 複数の<i>kbcallback Secondarydumpdata</i>ルーチンを登録するドライバーは、コールバックごとに一意の GUID を割り当てる必要があります。

<b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a></b>を使用して、 <i>Kb secondarydumpdata</i>ルーチンを登録します。 ドライバーは、その後、 <b><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a></b>ルーチンを使用してコールバックルーチンを削除できます。 ドライバーをアンロードできる場合は、その<i><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload">DRIVER_UNLOAD</a></i>コールバック関数で登録されているコールバックルーチンをすべて削除する必要があります。

<i>Kbの Secondarydumpdata</i>ルーチンは、実行できるアクションで非常に制限されています。 詳細については、「[バグチェックのコールバックルーチンの制限](#bug-check-callback-routine-restrictions)」を参照してください。

## <a name="implementing-a-kbcallbacktriagedumpdata-callback-routine"></a>Kbcallback Triagedumpdata コールバックルーチンの実装

Windows 10、バージョン1809、および Windows Server 2019 以降では、カーネルモードドライバーは、種類が*kbcallback Triagedumpdata*の[*KBUGCHECK_REASON_CALLBACK_ROUTINE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)コールバック関数を実装して、分割されたミニダンプファイルに仮想メモリ範囲を追加できます。 システムは、"指定された<i>データ</i>" パラメーターに、ダンプデータを記述する[**KBUGCHECK_TRIAGE_DUMP_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_triage_dump_data)構造体へのポインターを渡します。

次の例では、ドライバーによってトリアージダンプ配列が構成され、コールバックの最小実装が登録されます。

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
<i>Kb/Triagedumpdata</i>ルーチンは、実行できるアクションで非常に制限されています。 詳細については、「[バグチェックのコールバックルーチンの制限](#bug-check-callback-routine-restrictions)」を参照してください。

