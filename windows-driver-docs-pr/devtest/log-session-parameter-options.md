---
title: ログ セッション パラメーターのオプション
description: ログ セッション パラメーターのオプション
ms.assetid: 5398dfa7-abeb-443b-ab64-73b6599c8e73
keywords:
- トレース セッション WDK、詳細オプション
- WDK、ログ セッションのパラメーター オプションのセッションをトレースします。
- ログイン セッション パラメーター オプション WDK
- WDK のトレース フラグ
- WDK ソフトウェア トレースのフラグ
- 時間の WDK ソフトウェア トレースをフラッシュします。
- バッファーの WDK ソフトウェア トレース
- decay 時間 WDK ソフトウェア トレース
- 循環バッファ WDK ソフトウェア トレース
- グローバル シーケンス番号の WDK ソフトウェア トレース
- WDK のトレース レベル
- WDK ソフトウェア トレースのレベル
- WinDbg WDK ソフトウェア トレース
- 仮想ファイル WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ac2e3012702dc3124420f1b0b32e33a44052c35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548836"
---
# <a name="log-session-parameter-options"></a>ログ セッション パラメーターのオプション


**ログ セッションのパラメーター オプション** タブで、トレース セッションの変数の特徴の値を指定することができます。

設定し、トレース セッションを作成するときに、次のオプションの値を変更できます。 トレース セッションの実行中に、いくつかのオプションを変更できます。 変更不可能なオプションで使用できなくなります (「グレー」) を表示で、**ログ セッションのパラメーター オプション** ダイアログ ボックス。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**フラグ**  
指定します、[トレース フラグ](trace-flags.md)トレース プロバイダー。 トレース フラグは、プロバイダーが生成されるトレース メッセージを決定します。 フラグの意味は、各プロバイダーによって個別に決定されます。

Traceview でを見つけることができる場合、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)プロバイダーの選択フラグとレベルに表示されるリストから、**トレース フラグとレベル選択** ダイアログ ボックス。 開くには、**トレース フラグとレベルの選択**ダイアログ ボックスで、をクリックして、**設定**の値、**フラグ**または**レベル**オプション、 **ログ セッションのパラメーター オプション** ダイアログ ボックス。

<span id="Flush_Time__S_"></span><span id="flush_time__s_"></span><span id="FLUSH_TIME__S_"></span>**フラッシュ時間 (秒)**  
頻度を指定します (秒) をトレース セッションのトレース ログまたは traceview で表示するバッファーをフラッシュします。 既定では 1 (秒です)。

これらのフラッシュを強制は、フラッシュ バッファーがいっぱいのときに自動的に行われるだけでなく発生します。 値 0 は、強制フラッシュがないことを意味します。

1 秒ごとに 1 回よりも頻繁にフラッシュするには使用、**バッファー サイズ**各バッファーのサイズを小さくにはオプションです。

変更することができます、**フラッシュ時間**トレース セッションの実行中の値します。

<span id="Maximum_Buffers"></span><span id="maximum_buffers"></span><span id="MAXIMUM_BUFFERS"></span>**最大バッファー**  
トレース セッションで割り当てられるバッファーの最大数を指定します。

既定値は、プロセッサ、物理メモリの量と使用しているオペレーティング システムの数によって決まります。 トレース セッションの実行中に、この値を変更することができます。

<span id="Minimum_Buffers"></span><span id="minimum_buffers"></span><span id="MINIMUM_BUFFERS"></span>**最小バッファー**  
トレース メッセージを格納するため最初に割り当てられるバッファーの数を指定します。

バッファーの数で指定された値に到達するまで、多くのバッファーが割り当てられたバッファーがいっぱい、ときに、**最大バッファー**オプション。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。 トレース セッションの実行中に、この値を変更することはできません。

<span id="Buffer_Size"></span><span id="buffer_size"></span><span id="BUFFER_SIZE"></span>**バッファー サイズ**  
トレース セッションに割り当てられた各バッファーのサイズをキロバイト (KB) を指定します。 既定値は、プロセッサ、物理メモリの量と使用のオペレーティング システムの数によって決まります。 トレース セッションの実行中に、この値を変更することはできません。

<span id="Decay_Time__Minutes_"></span><span id="decay_time__minutes_"></span><span id="DECAY_TIME__MINUTES_"></span>**Decay 時間 (分)**  
(分単位) を使用していないトレース バッファーが保持される期間解放される前に指定します。 既定値は 15 です。 このオプションの値に表示されます、**年齢**の列、[トレース セッションの一覧](trace-session-list.md)します。

このパラメーターは、Windows 2000 でのみ有効です。 トレース セッションの実行中に、この値を変更することはできません。

<span id="Circular_Buffer_Size__MB_"></span><span id="circular_buffer_size__mb_"></span><span id="CIRCULAR_BUFFER_SIZE__MB_"></span>**循環バッファ サイズ (MB)**  
トレース バッファーが循環することを指定し、各バッファーの最大サイズ (単位は MB) を指定します。

循環バッファーがいっぱいになった場合は、最も古いトレース メッセージを上書きする、バッファーの先頭に新しいトレース メッセージが書き込まれます。 既定では、トレース バッファーは、順次、循環できません。

トレース セッションの実行中に、この値を変更することはできません。

<span id="Sequential_Buffer_Size__MB_"></span><span id="sequential_buffer_size__mb_"></span><span id="SEQUENTIAL_BUFFER_SIZE__MB_"></span>**シーケンシャルなバッファー サイズ (MB)**  
トレース バッファーがシーケンシャルで、各バッファーの最大サイズ (単位は MB) を指定するかどうかを指定します。

シーケンシャル バッファーがいっぱいになった場合、トレース メッセージは別のバッファーに書き込まれます。 または失われます。 既定では、トレース バッファーは、順次、循環しないられ、それぞれが 200 MB。

トレース セッションの実行中に、この値を変更することはできません。

<span id="Start_New_File_After_Buffer_Size__MB_"></span><span id="start_new_file_after_buffer_size__mb_"></span><span id="START_NEW_FILE_AFTER_BUFFER_SIZE__MB_"></span>**バッファー サイズ (MB) の後に新しいファイルを開始します。**  
既存のログが、指定した値に達するたびに、新しいトレース ログ ファイル (.etl) を作成します。 値は、各ログ ファイルの最大サイズを mb 単位で指定します。

このオプションの値に表示されます、**新しいファイル**の列、[トレース セッションの一覧](trace-session-list.md)します。

プロバイダーはときに生成するトレースのログは、選択した場合にのみ、このオプションは有効な[ログ トレース イベントのデータ ファイルのオプションを](basic-trace-session-options.md)上、**ログ セッション オプション**ページ。 このオプションは循環バッファーまたはログからの影響を与えません、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。 Windows 2000 ではサポートされません。

<span id="Use_Global_Sequence_Numbers"></span><span id="use_global_sequence_numbers"></span><span id="USE_GLOBAL_SEQUENCE_NUMBERS"></span>**グローバル シーケンス番号を使用します。**  
各トレース メッセージのグローバル シーケンス番号を生成します。

グローバル シーケンス番号は、コンピューター上のすべてのトレース セッションに一意です。 このオプションの既定値は**FALSE**します。

このオプションは、Windows 2000 ではサポートされていませんからのログに影響を与えません、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

<span id="Use_Local_Sequence_Number"></span><span id="use_local_sequence_number"></span><span id="USE_LOCAL_SEQUENCE_NUMBER"></span>**ローカルのシーケンス番号を使用して、**  
各トレース メッセージをローカルのシーケンス番号を生成します。 既定値は**TRUE**します。

ローカルのシーケンス番号は、トレース セッション内で一意です。

このオプションは、Windows 2000 ではサポートされていませんからのログに影響を与えません、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**レベル**  
指定します、[トレース レベル](trace-level.md)トレース プロバイダー。 トレース レベルは、プロバイダーが生成されるトレース メッセージを決定します。 レベル値の意味は、各プロバイダーによって個別に決まります。 通常、詳細のレベルの増加を表します。

Traceview でを見つけることができる場合、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)プロバイダーの選択フラグとレベルに表示されるリストから、**トレース フラグとレベル選択** ダイアログ ボックス。 開くには、**トレース フラグとレベルの選択**ダイアログ ボックスで、をクリックして、**設定**の値、**フラグ**または**レベル**オプション、 **ログ セッションのパラメーター オプション** ダイアログ ボックス。

トレース レベルの詳細については、の説明を参照して、 *EnableLevel*のパラメーター、 **EnableTrace** Microsoft Windows SDK 内の関数。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
リダイレクトは WinDbg、KD するメッセージをトレース traceview でウィンドウに表示する方法だけでなく、どちらが有効です。 このオプションは 3 KB、WinDbg で許可される最大サイズにも、バッファーのサイズを設定します。 表示される値、**バッファー サイズ**オプションは無視されます。

デバッガーでのトレース メッセージを表示するには、wmitrace.dll と traceprt.dll する必要がありますにホスト コンピューターで、デバッガーの検索パス。 これらの Dll が含まれている[ツールを Windows のデバッグ](https://go.microsoft.com/fwlink/p/?linkid=8708)も、検索するデバッガーを有効にする、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)、トレース メッセージの TMF ファイルは、デバッガーの検索である必要がありますホスト コンピューター上のパス。 デバッガーの検索パスを設定するには、使用、! wmitrace.searchpath デバッガー拡張機能を特殊化または % のトレースの値を設定\_形式\_検索\_%path% 環境変数。 WinDbg と WMI のトレースの拡張機能については、Windows のツールのデバッグを参照してください。

<span id="Ignore_TraceView"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**Traceview で無視します。**  
Traceview で操作の結果としてトレース メッセージを抑制します。

<span id="Virtual_File_Size"></span><span id="virtual_file_size"></span><span id="VIRTUAL_FILE_SIZE"></span>**仮想ファイルのサイズ**  
新しいメッセージを確保するために最も古いメッセージを上書きを開始する前に traceview で格納するトレース メッセージの最大数を示します。

値**0**最大値がないことを意味します。 Traceview では、すべてのメッセージを保持し、上書きすることはありません。 このオプションの既定値**65536**、ほとんどのシステムの推奨値です。 大きな値には、重要な遅延を引き起こす可能性があります。

この値に表示されます、**トレース レコードの最大**の列、[トレース セッションの一覧](trace-session-list.md)します。

 

 





