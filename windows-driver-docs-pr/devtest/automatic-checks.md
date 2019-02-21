---
title: 自動チェック
description: 自動チェック
ms.assetid: ec3cb6a4-d990-4830-914c-064f6c79371a
keywords:
- 自動チェック WDK Driver Verifier
- IRQL WDK Driver Verifier の監視
- スタックの WDK Driver Verifier の切り替え
- 空きプール タイマー WDK Driver Verifier
- クリーンアップするには、WDK の Driver Verifier を確認します。
- スタック WDK Driver Verifier の切り替え
- ドライバーは、WDK Driver Verifier をアンロードします。
- ドライバー検証ツールのオプション、IRQL の監視とメモリのルーチン
- ドライバー検証ツールのオプション、スタックの切り替えの監視
- Driver Verifier のオプション ドライバーのアンロードのチェック
- ドライバー検証ツールのオプション、ドライバーのディスパッチ ルーチンの監視
- ドライバー検証のオプション、使用状況の監視メモリ ディスパッチ一覧 (MDL)
ms.date: 10/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1345b51c6ba30a65991ed51cd7ec85ffd31016bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556561"
---
# <a name="automatic-checks"></a>自動チェック


## <span id="ddk_automatic_checks_tools"></span><span id="DDK_AUTOMATIC_CHECKS_TOOLS"></span>


Driver Verifier は、1 つまたは複数のドライバーを検証しているときに、次のチェックを実行します。 アクティブ化またはこれらのチェックを非アクティブ化することはできません。 以降、Windows 10 バージョン 1709 でこれらの自動チェックに関連する移動されました[標準フラグ](verifier-command-line.md)します。 結果として、標準のフラグでドライバーの検証を有効にするユーザーを確認できません削減チェックを適用します。

### <a name="span-idddkmonitoringirqlandmemoryroutinestoolsspanspan-idddkmonitoringirqlandmemoryroutinestoolsspanmonitoring-irql-and-memory-routines"></a><span id="ddk_monitoring_irql_and_memory_routines_tools"></span><span id="DDK_MONITORING_IRQL_AND_MEMORY_ROUTINES_TOOLS"></span>IRQL とメモリのルーチンの監視

Driver Verifier は、操作を許可されていない次の選択したドライバーを監視します。

-   IRQL を呼び出すことによって発生させる**KeLowerIrql**

-   IRQL を呼び出すことによって削減**KeRaiseIrql**

-   サイズがゼロ メモリの割り当てを要求します。

-   割り当てや解放 IRQL でページ プール&gt;APC\_レベル

-   割り当てや解放 IRQL で非ページ プール&gt;ディスパッチ\_レベル

-   前の割り当てから返されませんでしたアドレスを解放しようとしています。

-   既に解放されているアドレスを解放しようとしています。

-   取得または解放、IRQL で高速なミュー テックス&gt;APC\_レベル

-   取得またはディスパッチ等しく IRQL でスピン ロックを解放\_レベル

-   スピン ロックを二重解放します。

-   割り当て要求する必要がありますをマークする\_成功します。 このような要求は、これまでの許容ではありません。

ドライバーの検証ツールがアクティブでない場合は、これらの違反では、すべてのケースでは、即時のシステムのクラッシュ可能性がありますされません。 Driver Verifier は、ドライバーの動作を監視し、これらの違反が発生した場合、バグ チェック 0xC4 を発行します。 参照してください[**バグ チェック 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (ドライバー\_VERIFIER\_検出\_違反)、バグの一覧については、パラメーターを確認します。

### <a name="span-idddkmonitoringstackswitchingtoolsspanspan-idddkmonitoringstackswitchingtoolsspanmonitoring-stack-switching"></a><span id="ddk_monitoring_stack_switching_tools"></span><span id="DDK_MONITORING_STACK_SWITCHING_TOOLS"></span>スタックの切り替えの監視

Driver Verifier は、検証されているドライバーによって、スタックの使用状況を監視します。 そのスタックを切り替えるし、新しいスタックはスレッド スタックでも DPC スタック、バグ チェックが発行されます。 (このバグ チェックする 0xC4 0x90 と等しい最初のパラメーターを使用します。)によって表示されるスタック、 **KB**デバッガー コマンドがこの操作を実行したドライバーを通常表示されます。

### <a name="span-idddkcheckingondriverunloadtoolsspanspan-idddkcheckingondriverunloadtoolsspanchecking-on-driver-unload"></a><span id="ddk_checking_on_driver_unload_tools"></span><span id="DDK_CHECKING_ON_DRIVER_UNLOAD_TOOLS"></span>ドライバーのアンロードのチェック

されているドライバーのアンロードを検証した後、Driver Verifier は、ドライバーがクリーンアップされたことを確認するいくつかのチェックを実行します。

具体的には、Driver Verifier を検索します。

-   削除されていないタイマー

-   保留中の遅延プロシージャ呼び出し (Dpc)

-   削除の取り消しのルック アサイド リスト

-   削除されていないワーカー スレッド

-   キューの削除の取り消し

-   その他の同様のリソース

ドライバーのアンロードとチェックを決定することができます、これらのバグの原因の後に発行するためのチェックのバグなど、このシステムを引き起こす可能性の問題。 ドライバーの検証ツールがアクティブのときのバグ チェック xc 7 ドライバーが読み込まれる後すぐに発行されるこのような違反が発生します。 参照してください[**バグ チェック xc 7** ](https://msdn.microsoft.com/library/windows/hardware/ff560198) (タイマー\_または\_DPC\_が無効です)、バグの一覧については、パラメーターを確認します。


### <a name="span-idmonitoringmemorydescriptorlistmdlusagespanspan-idmonitoringmemorydescriptorlistmdlusagespanspan-idmonitoringmemorydescriptorlistmdlusagespanmonitoring-memory-descriptor-list-mdl-usage"></a><span id="Monitoring__Memory_Descriptor_List__MDL__Usage"></span><span id="monitoring__memory_descriptor_list__mdl__usage"></span><span id="MONITORING__MEMORY_DESCRIPTOR_LIST__MDL__USAGE"></span>メモリ記述子のリスト (MDL) の使用状況の監視

Windows Vista で、Driver Verifier は、操作を許可されていない次の選択したドライバーを監視します。

-   呼び出す[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)または適切なフラグがない、MDL で MmProbeAndLockProcessPages します。 たとえば、位置が正しくないを呼び出す**MmProbeAndLockPages**を使用して作成された、MDL の[ **MmBuildMdlForNonPagedPool**](https://msdn.microsoft.com/library/windows/hardware/ff554498)します。

-   呼び出す[ **MmMapLockedPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554622) MDL 適切なフラグがないのです。 たとえば、位置が正しくないを呼び出す**MmMapLockedPages**システム アドレスに既にマップされている、MDL のまたはと MDL ロックされていません。

-   呼び出す[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)または[ **MmUnmapLockedPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556391)部分的な MDL、つまりとを使用して作成された MDL [ **IoBuildPartialMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548324)します。

-   呼び出す**MmUnmapLockedPages** MDL システム アドレスにマップされていないのです。

ドライバーの検証ツールがアクティブでない場合は、これらの違反がすべてのケースですぐに応答を停止するシステムをされないことがあります。 Driver Verifier は、ドライバーの動作を監視し、これらの違反が発生した場合、バグ チェック 0xC4 を発行します。 参照してください[**バグ チェック 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (ドライバー\_VERIFIER\_検出\_違反)、バグの一覧については、パラメーターを確認します。

### <a name="span-idsynchronizationobjectallocationfromnonpagedpoolsessionmemoryspanspan-idsynchronizationobjectallocationfromnonpagedpoolsessionmemoryspanspan-idsynchronizationobjectallocationfromnonpagedpoolsessionmemoryspansynchronization-object-allocation-from-nonpagedpoolsession-memory"></a><span id="Synchronization_Object_Allocation_from_NonPagedPoolSession_Memory"></span><span id="synchronization_object_allocation_from_nonpagedpoolsession_memory"></span><span id="SYNCHRONIZATION_OBJECT_ALLOCATION_FROM_NONPAGEDPOOLSESSION_MEMORY"></span>NonPagedPoolSession メモリから同期オブジェクトの割り当て

Windows 7 以降、Driver Verifier は、セッションのメモリからの同期オブジェクトをチェックします。

同期オブジェクトは、非ページングである必要があります。 また、グローバル システム全体の仮想アドレス空間内に存在する必要があります。

グラフィックス ドライバーなどで Api を呼び出すことによって、セッション メモリを割り当てることができます[ **EngAllocMem**](https://msdn.microsoft.com/library/windows/hardware/ff564176)します。 、グローバル アドレス空間とは異なり、各ターミナル サーバー セッションのセッションのアドレス空間が仮想化します。 これは、2 つの異なるセッションのコンテキストで使用されている同じ仮想アドレスが 2 つの異なるオブジェクトを指すことを意味します。 Windows カーネルは、任意のターミナル サーバー セッションからの同期オブジェクトにアクセスできる必要があります。 システムがクラッシュまたは別のセッションのデータの破損をサイレントなどの予期しない結果には、別のセッションからセッションのメモリ アドレスを参照しようとしています。

Windows 7 以降、ときに検証済みのドライバーを初期化します Api を呼び出すことによって、同期オブジェクトなど[ **KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137)または[ **KeInitializeMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff552147)、Driver Verifier は、セッションの仮想アドレス空間内でオブジェクトのアドレスがあるかどうかを確認します。 Driver Verifier は、この種の不適切なアドレスを検出する場合は、発行、 [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)、0 xdf のパラメーター 1 の値。

### <a name="span-idobjectreferencecounterchangesfrom0to1spanspan-idobjectreferencecounterchangesfrom0to1spanspan-idobjectreferencecounterchangesfrom0to1spanobject-reference-counter-changes-from-0-to-1"></a><span id="Object_Reference_Counter_Changes_from_0_to_1"></span><span id="object_reference_counter_changes_from_0_to_1"></span><span id="OBJECT_REFERENCE_COUNTER_CHANGES_FROM_0_TO_1"></span>オブジェクトの参照カウンターが 0 から 1 に変更します。

Windows 7 以降、Driver Verifier は、不正なオブジェクト参照の追加のクラスをチェックします。

Windows カーネル オブジェクト マネージャーは、ファイル オブジェクトまたはスレッド オブジェクトなどのオブジェクトを作成するときに、新しいオブジェクトの参照カウンターが 1 に設定されます。 などの参照カウンターが Api の呼び出しで増やされます[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)または[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679). 参照カウンターがだけデクリメントした各[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)同じオブジェクトに対して呼び出します。

参照カウンターには、値 0 に達すると、オブジェクトが解放する対象となります。 オブジェクト マネージャーが、すぐに解放可能性があるか、後では無料可能性があります。 呼び出す[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)または[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)および 0 から 1 をへの参照カウンターの変更既に解放されたオブジェクトの参照カウンターをインクリメントします。 これは、常に正しくない他のユーザーのメモリ割り当てが破損する可能性があるためです。

### <a name="span-idsystemshutdownblocksordelaysspanspan-idsystemshutdownblocksordelaysspanspan-idsystemshutdownblocksordelaysspansystem-shutdown-blocks-or-delays"></a><span id="System_Shutdown_Blocks_or_Delays"></span><span id="system_shutdown_blocks_or_delays"></span><span id="SYSTEM_SHUTDOWN_BLOCKS_OR_DELAYS"></span>システム シャット ダウンはブロックや遅延

Windows 7 以降、Driver verifier 区切りをカーネル デバッガーにシステムのシャット ダウンが開始された後、20 分に完了しない場合。 Driver Verifier は、Windows カーネルが、レジストリ、プラグ アンド プレイでは、I/O マネージャー サブシステムなど、さまざまなサブシステムをシャット ダウンを開始する時刻としてシステムのシャット ダウンの開始を割り当てます。

Driver Verifier の問題をシステムにカーネル デバッガーがアタッチされていない場合、 [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)パラメーター 1 値はこのブレークポイントではなく、0x115 です。

頻繁に 20 分もかからずに完了できないシステムのシャット ダウンでは、そのシステムで実行されているドライバーのいずれかが故障していることを示します。 実行している **! 分析-v**カーネル デバッガーがシャット ダウンを担当するシステム ワーカー スレッドのスタック トレースを表示します。 そのスタック トレースを調べるし、テスト中のドライバーのいずれかでシャット ダウンのスレッドがブロックされているかどうかを判断する必要があります。

場合があります、システムをシャット ダウンできない負荷の大きいテストの対象となっている、すべてのドライバーが正しく機能している場合でもです。 ユーザーは、この Driver Verifier のブレークポイントの後の実行を継続し、システムが最終的にシャット ダウンするかどうかを確認できます。

 

 





