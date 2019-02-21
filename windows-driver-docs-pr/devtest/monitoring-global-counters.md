---
title: グローバル カウンターの監視
description: グローバル カウンターの監視
ms.assetid: ca8f2b87-bb62-4389-bd59-1ed8ef6ac730
keywords:
- グローバル カウンター WDK Driver Verifier
- Driver Verifier の WDK、カウンター
- WDK の Driver Verifier の統計情報
- WDK の Driver Verifier のカウンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d248ae19b177ce8a55003bf7387dcabcda823fcf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551394"
---
# <a name="monitoring-global-counters"></a>グローバル カウンターの監視


## <span id="ddk_monitoring_global_counters_tools"></span><span id="DDK_MONITORING_GLOBAL_COUNTERS_TOOLS"></span>


*グローバル カウンター*のドライバーをドライバーの検証を実行するアクションを監視する統計します。 これらの統計情報が検証されているすべてのドライバーから描画されます。

グローバル カウンターを使用して表示することができます、 [ **Verifier のコマンド ライン**](verifier-command-line.md)、またはドライバー検証マネージャーを使用しています。 2 つのバージョンのドライバー検証マネージャー--に 1 つずつ[Windows 2000](driver-verifier-manager--windows-2000-.md)とに 1 つずつ[Windows XP 以降](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>検証ツールのコマンドライン

グローバル カウンターを表示する、 **verifier/query**コマンド。 両方のグローバル カウンターが表示されますおよび[個々 のカウンター](monitoring-individual-counters.md)します。

Driver Verifier にグローバル カウンターが含まれるも[ログ ファイル](creating-log-files.md)します。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>ドライバー検証マネージャー (Windows 2000)

グローバル カウンターを表示するには、選択、**グローバル カウンター**タブ。このタブには、ほぼすべてのグローバル カウンターが含まれます。 (ただし、**割り当てのない追跡**カウンターでは、**プール追跡**画面、および特別なプールの 95% のアラートは、 **ドライバ ステータスの**の説明に従って、画面すぐ下にします)。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>ドライバー検証マネージャー (Windows XP 以降)

グローバル カウンターを表示するには、ドライバー検証マネージャーを起動し、選択、**現在検証済みのドライバーに関する情報を表示**タスク。 キーを押します**次**2 回クリックします。

### <a name="span-idexplanationofglobalcountersspanspan-idexplanationofglobalcountersspanexplanation-of-global-counters"></a><span id="explanation_of_global_counters"></span><span id="EXPLANATION_OF_GLOBAL_COUNTERS"></span>グローバル カウンターの説明

次のグローバルなカウンターの監視に関連する統計、[強制 IRQL 検査](force-irql-checking.md)オプション。 これらのカウンターには、現在検証されているすべてのカーネル モード ドライバーによって最後の起動後に実行されたアクションが含まれます。

<span id="IRQL_Raises"></span><span id="irql_raises"></span><span id="IRQL_RAISES"></span>**IRQL が発生します**  
回数の合計は、ドライバーには、IRQL が発生したことを確認します。

<span id="Spinlocks_Acquired"></span><span id="spinlocks_acquired"></span><span id="SPINLOCKS_ACQUIRED"></span>**スピンロックが獲得**  
回数の合計は、スピン ロックを取得したドライバーを確認します。

<span id="Executions_Synchronized"></span><span id="executions_synchronized"></span><span id="EXECUTIONS_SYNCHRONIZED"></span>**同期の実行**  
回数の合計は、ドライバーでは、割り込みを特定のオブジェクト ポインターに関連付けられている ISR を指定したルーチンの実行が同期されていることを確認します。

<span id="Trims"></span><span id="trims"></span><span id="TRIMS"></span>**トリム**  
Driver Verifier ワーキング セットからページング可能なメモリをトリミングする回数。 (トリム ページの数ではなく、ドライバーの検証ツールによって行われたトリミング パスの数は、このことに注意してください)。

次にグローバル カウンターの監視に関連する統計情報、[低リソース シミュレーション](low-resources-simulation.md)オプション。

<span id="Faults_Injected"></span><span id="faults_injected"></span><span id="FAULTS_INJECTED"></span>**エラーの挿入**  
最後の起動後、Driver Verifier によって意図的に失敗、リソース割り当ての合計数。

次のグローバルなカウンターの監視に関連する統計、[特別なプール](special-pool.md)オプション。 これらのカウンターは、常に現在検証されているすべてのカーネル モード ドライバーの起動後しようとした割り当てを反映します。

<span id="Pool_Allocations_Attempted"></span><span id="pool_allocations_attempted"></span><span id="POOL_ALLOCATIONS_ATTEMPTED"></span>**プール割り当ての試行**  
これらのドライバーが試行したメモリ割り当ての合計数。

<span id="Pool_Allocations_Succeeded"></span><span id="pool_allocations_succeeded"></span><span id="POOL_ALLOCATIONS_SUCCEEDED"></span>**プールの割り当てに成功しました**  
割り当ての数は、成功したことを試みます。

<span id="Pool_Allocations_Succeeded_in_Special_Pool"></span><span id="pool_allocations_succeeded_in_special_pool"></span><span id="POOL_ALLOCATIONS_SUCCEEDED_IN_SPECIAL_POOL"></span>**プール割り当ての特別なプールに成功しました**  
割り当ての試行が成功した、特別なプールから割り当てられた番号。

<span id="Pool_Allocations_Without_Tag"></span><span id="pool_allocations_without_tag"></span><span id="POOL_ALLOCATIONS_WITHOUT_TAG"></span>**タグのないプールの割り当て**  
数はこれらのドライバーの要求されたメモリ割り当ての時間が、プール タグが指定されていません。 (プール タグは常に推奨のすべての割り当て)。

<span id="Pool_Allocations_Failed"></span><span id="pool_allocations_failed"></span><span id="POOL_ALLOCATIONS_FAILED"></span>**プールの割り当てに失敗しました**  
割り当ての数は、失敗した原因がメモリの不足しているしようとします。

特別なプール機能が有効になっているすべてのプール割り当ての 95% 未満を特別なプールから割り当てられている場合は、警告が表示されます。 Windows XP 以降では、この警告に表示されます ダイアログ ボックス、**グローバル カウンター**画面。 Windows 2000 でこの警告が表示されます、 **ドライバ ステータスの**画面。

次にグローバル カウンターの監視に関連する統計情報、[特別なプール](special-pool.md)と[プール追跡](pool-tracking.md)オプション。 プールの追跡がアクティブでない場合は 0 常になります。

<span id="Pool_Allocations_Not_Tracked"></span><span id="pool_allocations_not_tracked"></span><span id="POOL_ALLOCATIONS_NOT_TRACKED"></span>**プールの割り当ては追跡されません。**  
現在検証されているすべてのドライバーからの追跡対象でない割り当ての数。 サイズが 1 つのページまたは拡大はできませんの割り当ては、プールの追跡によって追跡され、特別なプールから割り当てられることはできません。 [個々 のカウンター](monitoring-individual-counters.md)これらの割り当ては反映されません。 (で Windows 2000 では、このカウンターを確認できます、**プール追跡**タイトルの下の画面**割り当てのない追跡**)。

 

 





