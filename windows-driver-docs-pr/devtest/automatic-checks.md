---
title: 自動チェック
description: 自動チェック
ms.assetid: ec3cb6a4-d990-4830-914c-064f6c79371a
keywords:
- WDK ドライバーの検証ツールを自動的にチェックする
- IRQL 監視 WDK ドライバー検証ツール
- スタック切り替え WDK ドライバー検証ツール
- 無料プールタイマー WDK ドライバー検証ツール
- クリーンアップチェック WDK ドライバー検証ツール
- スタックを切り替える WDK ドライバーの検証ツール
- ドライバーが WDK ドライバー検証ツールをアンロードする
- ドライバーの検証ツールのオプション、IRQL およびメモリルーチンの監視
- ドライバーの検証ツールのオプション、スタックの切り替えの監視
- ドライバーの検証ツールのオプション、ドライバーのアンロードを確認しています
- ドライバーの検証ツールのオプション、ドライバーのディスパッチルーチンの監視
- ドライバー検証ツールのオプション、メモリディスパッチリスト (MDL) の使用状況の監視
ms.date: 10/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7415fca6178920989000a14052c05a7b90a77e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840305"
---
# <a name="automatic-checks"></a>自動チェック


## <span id="ddk_automatic_checks_tools"></span><span id="DDK_AUTOMATIC_CHECKS_TOOLS"></span>


ドライバーの検証ツールは、1つまたは複数のドライバーを確認するたびに、次のチェックを実行します。 これらのチェックをアクティブ化または非アクティブ化することはできません。 Windows 10 バージョン1709以降では、これらの自動チェックは関連する[標準フラグ](verifier-command-line.md)に移動されています。 その結果、標準フラグを使用してドライバーの検証機能を有効にすると、チェックが適用されていないことがわかります。

### <a name="span-idddk_monitoring_irql_and_memory_routines_toolsspanspan-idddk_monitoring_irql_and_memory_routines_toolsspanmonitoring-irql-and-memory-routines"></a><span id="ddk_monitoring_irql_and_memory_routines_tools"></span><span id="DDK_MONITORING_IRQL_AND_MEMORY_ROUTINES_TOOLS"></span>IRQL とメモリルーチンの監視

ドライバーの検証ツールは、選択したドライバーの次の禁止された操作を監視します。

-   **Kelowerirql**を呼び出して irql を上げる

-   **Keraiseirql**を呼び出して irql を下げる

-   サイズ0のメモリ割り当てを要求しています

-   IRQL &gt; APC\_レベルでのページプールの割り当てまたは解放

-   IRQL &gt; ディスパッチ\_レベルで、非ページプールの割り当てまたは解放を行う

-   以前の割り当てから返されなかったアドレスを解放しようとしています

-   既に解放されているアドレスを解放しようとしています

-   IRQL &gt; APC\_レベルで高速ミューテックスを取得または解放する

-   IRQL がディスパッチ\_レベルと等しくないスピンロックの取得または解放

-   スピンロックを二重に解放します。

-   割り当て要求をマークする\_成功する必要があります。 このような要求は一切許可されません。

ドライバーの検証ツールがアクティブでない場合、これらの違反によってシステムが即座にクラッシュすることはありません。 ドライバーの検証ツールは、ドライバーの動作を監視し、これらの違反が発生した場合は、バグチェック0xC4 を発行します。 バグチェックパラメーターの一覧については、「[**バグチェック 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (ドライバー\_VERIFIER\_検出された\_違反)」を参照してください。

### <a name="span-idddk_monitoring_stack_switching_toolsspanspan-idddk_monitoring_stack_switching_toolsspanmonitoring-stack-switching"></a><span id="ddk_monitoring_stack_switching_tools"></span><span id="DDK_MONITORING_STACK_SWITCHING_TOOLS"></span>スタック切り替えの監視

ドライバーの検証ツールは、検証されているドライバーによってスタックの使用状況を監視します。 ドライバーがスタックを切り替え、新しいスタックがスレッドスタックでも DPC スタックでもない場合は、バグチェックが発行されます。 (これは、最初のパラメーターが0x90 に等しいバグチェック0xC4 になります)。**KB**デバッガーコマンドによって表示されるスタックは、通常、この操作を実行したドライバーを明らかにします。

### <a name="span-idddk_checking_on_driver_unload_toolsspanspan-idddk_checking_on_driver_unload_toolsspanchecking-on-driver-unload"></a><span id="ddk_checking_on_driver_unload_tools"></span><span id="DDK_CHECKING_ON_DRIVER_UNLOAD_TOOLS"></span>ドライバーのアンロードを確認しています

検証されているドライバーがアンロードされた後、ドライバーの検証ツールは、ドライバーがクリーンアップされたことを確認するためにいくつかのチェックを実行します。

特に、Driver Verifier は次のものを検索します。

-   タイマーの取り消しの取り消し

-   保留中の遅延プロシージャ呼び出し (Dpc)

-   ルックアサイドリストの取り消し

-   ワーカースレッドの取り消しの取り消し

-   キューの取り消し

-   その他の類似リソース

このような問題によって、ドライバーがアンロードされた後にシステムのバグチェックが発生する可能性があり、これらのバグチェックの原因を特定するのが困難になる可能性があります。 ドライバーの検証ツールがアクティブになっていると、このような違反が発生すると、ドライバーがアンロードされた直後にバグチェック0xC7 が発行されます。 バグチェックパラメーターの一覧については、「[**バグチェック 0xC7**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc7--timer-or-dpc-invalid) (タイマー\_または\_DPC\_無効)」を参照してください。


### <a name="span-idmonitoring__memory_descriptor_list__mdl__usagespanspan-idmonitoring__memory_descriptor_list__mdl__usagespanspan-idmonitoring__memory_descriptor_list__mdl__usagespanmonitoring-memory-descriptor-list-mdl-usage"></a><span id="Monitoring__Memory_Descriptor_List__MDL__Usage"></span><span id="monitoring__memory_descriptor_list__mdl__usage"></span><span id="MONITORING__MEMORY_DESCRIPTOR_LIST__MDL__USAGE"></span>メモリ記述子リスト (MDL) の使用状況の監視

Windows Vista では、ドライバーの検証ツールは、選択したドライバーが次の許可されていない操作を監視することもあります。

-   適切なフラグが設定されていない MDL で[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)または MmProbeAndLockProcessPages を呼び出しています。 たとえば、 [**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)を使用して作成された MDL の**MmProbeAndLockPages**を呼び出すことは正しくありません。

-   適切なフラグが設定されていない MDL で[**MmMapLockedPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages)を呼び出しています。 たとえば、システムアドレス、またはロックされていない MDL に既にマップされている MDL に対して**MmMapLockedPages**を呼び出すことは、正しくありません。

-   [**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)または[**MmUnmapLockedPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages)を部分的な Mdl (つまり、 [**iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)を使用して作成された mdl) で呼び出す。

-   システムアドレスにマップされていない MDL で**MmUnmapLockedPages**を呼び出しています。

Driver Verifier がアクティブでない場合、このような違反が発生しても、システムがすぐに応答を停止することはありません。 ドライバーの検証ツールは、ドライバーの動作を監視し、これらの違反が発生した場合は、バグチェック0xC4 を発行します。 バグチェックパラメーターの一覧については、「[**バグチェック 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (ドライバー\_VERIFIER\_検出された\_違反)」を参照してください。

### <a name="span-idsynchronization_object_allocation_from_nonpagedpoolsession_memoryspanspan-idsynchronization_object_allocation_from_nonpagedpoolsession_memoryspanspan-idsynchronization_object_allocation_from_nonpagedpoolsession_memoryspansynchronization-object-allocation-from-nonpagedpoolsession-memory"></a><span id="Synchronization_Object_Allocation_from_NonPagedPoolSession_Memory"></span><span id="synchronization_object_allocation_from_nonpagedpoolsession_memory"></span><span id="SYNCHRONIZATION_OBJECT_ALLOCATION_FROM_NONPAGEDPOOLSESSION_MEMORY"></span>NonPagedPoolSession メモリからの同期オブジェクトの割り当て

Windows 7 以降では、ドライバーの検証ツールは、セッションメモリから同期オブジェクトを確認します。

同期オブジェクトは非ページングである必要があります。 また、グローバルなシステム全体の仮想アドレス空間にも存在する必要があります。

グラフィックスドライバーは、 [**EngAllocMem**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)などの api を呼び出すことによって、セッションメモリを割り当てることができます。 グローバルアドレス空間とは異なり、セッションアドレス空間は、各ターミナルサーバーセッションに対して仮想化されます。 これは、2つの異なるセッションのコンテキストで使用される同じ仮想アドレスが、2つの異なるオブジェクトを参照することを意味します。 Windows カーネルは、任意のターミナルサーバーセッションから同期オブジェクトにアクセスできる必要があります。 別のセッションからセッションメモリアドレスを参照しようとすると、システムのクラッシュや別のセッションのデータのサイレント破損など、予期しない結果が発生します。

Windows 7 以降では、検証されたドライバーが[**Keinitializeevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)や[**KeInitializeMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializemutex)などの api を呼び出すことによって同期オブジェクトを初期化するときに、ドライバーの検証ツールは、オブジェクトのアドレスがセッション仮想内にあるかどうかを確認します。アドレス空間。 Driver Verifier がこの種の不適切なアドレスを検出すると、[**バグチェック 0xC4: driver\_Verifier\_検出さ**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)れ、パラメーター1の値が0xDF であることが\_検出されます。

### <a name="span-idobject_reference_counter_changes_from_0_to_1spanspan-idobject_reference_counter_changes_from_0_to_1spanspan-idobject_reference_counter_changes_from_0_to_1spanobject-reference-counter-changes-from-0-to-1"></a><span id="Object_Reference_Counter_Changes_from_0_to_1"></span><span id="object_reference_counter_changes_from_0_to_1"></span><span id="OBJECT_REFERENCE_COUNTER_CHANGES_FROM_0_TO_1"></span>オブジェクト参照カウンターが0から1に変更される

Windows 7 以降では、ドライバーの検証ツールによって、誤ったオブジェクト参照の追加クラスが確認されます。

Windows カーネルオブジェクトマネージャーが、ファイルオブジェクトやスレッドオブジェクトなどのオブジェクトを作成すると、新しいオブジェクトの参照カウンターが1に設定されます。 参照カウンターは、 [**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)や[**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)などの api を呼び出すことによってインクリメントされます。 参照カウンターは、同じオブジェクトのすべての[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)呼び出しによってデクリメントされます。

参照カウンターが0の値に達すると、オブジェクトは解放されることになります。 オブジェクトマネージャーによってすぐに解放される場合もあれば、後で解放される場合もあります。 [**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)または[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出し、参照カウンターを0から1に変更することは、既に解放されているオブジェクトの参照カウンターをインクリメントすることを意味します。 これは、他のユーザーのメモリ割り当てが破損する可能性があるため、常に間違っています。

### <a name="span-idsystem_shutdown_blocks_or_delaysspanspan-idsystem_shutdown_blocks_or_delaysspanspan-idsystem_shutdown_blocks_or_delaysspansystem-shutdown-blocks-or-delays"></a><span id="System_Shutdown_Blocks_or_Delays"></span><span id="system_shutdown_blocks_or_delays"></span><span id="SYSTEM_SHUTDOWN_BLOCKS_OR_DELAYS"></span>システムシャットダウンのブロックまたは遅延

Windows 7 以降では、システムのシャットダウンが開始してから20分が経過していない場合、ドライバーの検証ツールはカーネルデバッガーの中断を発行します。 ドライバーの検証ツールは、レジストリ、プラグアンドプレイ、i/o マネージャーサブシステムなど、Windows カーネルがさまざまなサブシステムのシャットダウンを開始する時刻として、システムシャットダウンの開始を割り当てます。

カーネルデバッガーがシステムにアタッチされていない場合、ドライバーの検証ツールはバグチェックを発行します[**0xC4: driver\_Verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)は、このブレークポイントではなく、パラメーター1の値0x115 を使用して\_違反を検出\_ます。

多くの場合、システムのシャットダウンが20分未満で完了しないということは、そのシステムで実行されているドライバーの1つが誤動作していることを意味します。 カーネルデバッガーから **! analyze-v**を実行すると、シャットダウンの原因となっているシステムワーカースレッドのスタックトレースが表示されます。 このスタックトレースを調べて、テスト対象のドライバーのいずれかによってシャットダウンスレッドがブロックされているかどうかを確認する必要があります。

すべてのドライバーが正常に機能しているにもかかわらず、負荷の高いテストの対象となるため、システムをシャットダウンできないことがあります。 ユーザーは、このドライバー検証ツールのブレークポイントの後に実行を継続し、システムが最終的にシャットダウンするかどうかを確認できます。

 

 





