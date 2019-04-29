---
title: 個別カウンターの監視
description: 個別カウンターの監視
ms.assetid: 95d4492b-20b9-401a-97aa-eaf700b64420
keywords:
- 個々 のカウンター WDK Driver Verifier
- Driver Verifier の WDK、カウンター
- WDK の Driver Verifier の統計情報
- WDK の Driver Verifier のカウンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38eca341c7ad8773b27f16f5886e018e3b9c8b19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391322"
---
# <a name="monitoring-individual-counters"></a>個別カウンターの監視


## <span id="ddk_monitoring_individual_counters_tools"></span><span id="DDK_MONITORING_INDIVIDUAL_COUNTERS_TOOLS"></span>


*個々 のカウンター*のドライバーをドライバーの検証を実行するアクションを監視する統計します。 これらの統計情報は、検証されているドライバーごとに個別に保持されます。

使用して個々 のカウンターを表示できます、 [ **Verifier のコマンド ライン**](verifier-command-line.md)、またはドライバー検証マネージャーを使用しています。 2 つのバージョンのドライバー検証マネージャー--に 1 つずつ[Windows 2000](driver-verifier-manager--windows-2000-.md)とに 1 つずつ[Windows XP 以降](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>検証ツールのコマンドライン

個々 のカウンターを表示する、 **verifier/query**コマンド。 両方の個々 のカウンターが表示されますおよび[グローバル カウンター](monitoring-global-counters.md)します。

Driver Verifier で個々 のカウンターが含まれるも[ログ ファイル](creating-log-files.md)します。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>ドライバー検証マネージャー (Windows 2000)

個々 のカウンターを表示するには、選択、**プール追跡**タブ。ドロップダウン ボックスから、目的のドライバーを選択します。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>ドライバー検証マネージャー (Windows XP 以降)

個々 のカウンターを表示するには、ドライバー検証マネージャーを起動し、選択、**現在検証済みのドライバーに関する情報を表示**タスク。 キーを押します**次**3 回です。

最後に、ドロップダウン ボックスから、目的のドライバーを選択します。

### <a name="span-idexplanationofindividualcountersspanspan-idexplanationofindividualcountersspanexplanation-of-individual-counters"></a><span id="explanation_of_individual_counters"></span><span id="EXPLANATION_OF_INDIVIDUAL_COUNTERS"></span>個々 のカウンターの説明

個々 のカウンターに関連する統計の監視、[プール追跡](pool-tracking.md)オプション。 これらすべて 0 になりますこのオプションがアクティブでない場合です。

これらの統計情報は、2 つのセクションに分けられます。**ページ プール**と**非ページ プール**します。 メモリ プールの各種類では、次の 4 つのカウンターが表示されます。

<span id="Current_Number_of_Allocations"></span><span id="current_number_of_allocations"></span><span id="CURRENT_NUMBER_OF_ALLOCATIONS"></span>**現在の割り当ての数**  
この種類のメモリ プールから指定されたドライバーによって行われた個々 の割り当ての現在数。

<span id="Peak_Number_of_Allocations"></span><span id="peak_number_of_allocations"></span><span id="PEAK_NUMBER_OF_ALLOCATIONS"></span>**割り当ての最大数**  
この種類のメモリ プールから、指定したドライバーでの起動後に常に行われた個々 の割り当ての最大数。

<span id="Current_Bytes_Allocated"></span><span id="current_bytes_allocated"></span><span id="CURRENT_BYTES_ALLOCATED"></span>**割り当てられている現在のバイト数**  
現在この種類のメモリ プールから指定されたドライバーに割り当てられたバイト数。

<span id="Peak_Bytes_Allocated"></span><span id="peak_bytes_allocated"></span><span id="PEAK_BYTES_ALLOCATED"></span>**割り当てられたバイト数のピーク**  
この種類のメモリ プールから指定されたドライバーの起動後に常に割り当てられたバイトの最大数。

サイズが 1 つのページまたは拡大はできませんの割り当ては、プールの追跡によって追跡され、特別なプールから割り当てられることはできません。 これらの個々 のカウンターは、これらの大きな割り当てには反映されません。 このようなすべての割り当ての数がわかるように、[グローバル カウンター](monitoring-global-counters.md)します。

 

 





