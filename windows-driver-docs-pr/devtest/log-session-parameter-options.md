---
title: ログ セッション パラメーターのオプション
description: ログ セッション パラメーターのオプション
ms.assetid: 5398dfa7-abeb-443b-ab64-73b6599c8e73
keywords:
- トレースセッション WDK、詳細オプション
- トレースセッション WDK、ログセッションパラメーターオプション
- ログセッションパラメーターオプション WDK
- トレースフラグ WDK
- WDK ソフトウェアのトレースに関するフラグ
- フラッシュ時間 WDK ソフトウェアのトレース
- WDK ソフトウェアトレースのバッファー
- 減衰時間 WDK ソフトウェアのトレース
- 循環バッファー WDK ソフトウェアトレース
- グローバルシーケンス番号 WDK ソフトウェアトレース
- トレースレベル WDK
- レベル WDK ソフトウェアトレース
- WinDbg WDK ソフトウェアのトレース
- 仮想ファイル WDK ソフトウェアのトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2eca69ddc8790136bc9c26e996dbf989afe25f6
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769638"
---
# <a name="log-session-parameter-options"></a>ログ セッション パラメーターのオプション


[**ログセッションパラメーターのオプション**] タブでは、トレースセッションの変数機能の値を指定できます。

トレースセッションの作成中に、次のオプションの値を設定および変更できます。 トレースセッションの実行中に、いくつかのオプションを変更できます。 [**ログセッションパラメーターのオプション**] ダイアログボックスで、変更できないオプションが淡色表示になります ("グレー表示")。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**示す**  
トレースプロバイダーの[トレースフラグ](trace-flags.md)を指定します。 トレースフラグは、プロバイダーが生成するトレースメッセージを決定します。 フラグの意味は、各プロバイダーによって個別に決定されます。

TraceView がプロバイダーの[トレースメッセージコントロール (tmc) ファイル](trace-message-control-file.md)を見つけることができる場合は、[**トレースフラグとレベルの選択**] ダイアログボックスに表示される一覧からフラグとレベルを選択できます。 [**トレースフラグとレベルの選択**] ダイアログボックスを開くには、[**ログセッションパラメーターのオプション**] ダイアログボックスの [**フラグ**または**レベル**] オプションの**設定**値をクリックします。

<span id="Flush_Time__S_"></span><span id="flush_time__s_"></span><span id="FLUSH_TIME__S_"></span>**フラッシュ時間 (秒)**  
トレースセッションバッファーをトレースログまたは TraceView 表示にフラッシュする頻度 (秒単位) を指定します。 既定値は 1 (秒) です。

これらの強制フラッシュは、バッファーがいっぱいになったときに自動的に発生するフラッシュに加えて発生します。 値0は強制的にフラッシュしないことを意味します。

1秒間に1回以上フラッシュするには、[**バッファーサイズ**] オプションを使用して各バッファーのサイズを小さくします。

トレースセッションの実行中に**フラッシュ時間**の値を変更できます。

<span id="Maximum_Buffers"></span><span id="maximum_buffers"></span><span id="MAXIMUM_BUFFERS"></span>**最大バッファー数**  
トレースセッションに割り当てられるバッファーの最大数を指定します。

既定値は、プロセッサの数、物理メモリの量、および使用しているオペレーティングシステムによって決まります。 この値は、トレースセッションの実行中に変更できます。

<span id="Minimum_Buffers"></span><span id="minimum_buffers"></span><span id="MINIMUM_BUFFERS"></span>**最小バッファー**  
トレースメッセージを格納するために最初に割り当てられるバッファーの数を指定します。

バッファーがいっぱいになると、バッファー数が**最大バッファー**オプションで指定された値に達するまで、より多くのバッファーが割り当てられます。 既定値は、プロセッサの数、物理メモリの量、および使用されているオペレーティングシステムによって決まります。 トレースセッションの実行中にこの値を変更することはできません。

<span id="Buffer_Size"></span><span id="buffer_size"></span><span id="BUFFER_SIZE"></span>**バッファーサイズ**  
トレースセッションに割り当てられている各バッファーのサイズ (KB 単位) を指定します。 既定値は、プロセッサの数、物理メモリの量、および使用されているオペレーティングシステムによって決まります。 トレースセッションの実行中にこの値を変更することはできません。

<span id="Decay_Time__Minutes_"></span><span id="decay_time__minutes_"></span><span id="DECAY_TIME__MINUTES_"></span>**減衰時間 (分)**  
未使用のトレースバッファーが解放されるまでの経過時間 (分) を指定します。 既定値は 15 です。 このオプションの値は、[[トレースセッション] の一覧](trace-session-list.md)の [ **Age** ] 列に表示されます。

このパラメーターは、Windows 2000 でのみ有効です。 トレースセッションの実行中にこの値を変更することはできません。

<span id="Circular_Buffer_Size__MB_"></span><span id="circular_buffer_size__mb_"></span><span id="CIRCULAR_BUFFER_SIZE__MB_"></span>**円形バッファーサイズ (MB)**  
トレースバッファーが循環することを指定し、各バッファーの最大サイズ (MB 単位) を指定します。

循環バッファーがいっぱいになると、新しいトレースメッセージがバッファーの先頭に書き込まれ、最も古いトレースメッセージが上書きされます。 既定では、トレースバッファーは循環ではなく順次です。

トレースセッションの実行中にこの値を変更することはできません。

<span id="Sequential_Buffer_Size__MB_"></span><span id="sequential_buffer_size__mb_"></span><span id="SEQUENTIAL_BUFFER_SIZE__MB_"></span>**シーケンシャルバッファーサイズ (MB)**  
トレースバッファーがシーケンシャルであるかどうかを指定し、各バッファーの最大サイズ (MB 単位) を指定します。

シーケンシャルバッファーがいっぱいになると、トレースメッセージは別のバッファーに書き込まれるか、または失われます。 既定では、トレースバッファーは、循環ではなく順次であり、それぞれ 200 MB です。

トレースセッションの実行中にこの値を変更することはできません。

<span id="Start_New_File_After_Buffer_Size__MB_"></span><span id="start_new_file_after_buffer_size__mb_"></span><span id="START_NEW_FILE_AFTER_BUFFER_SIZE__MB_"></span>**バッファーサイズ (MB) 後に新しいファイルを開始する**  
既存のログが指定された値に到達するたびに、新しいトレースログファイル (.etl) を作成します。 この値は、各ログファイルの最大サイズを MB 単位で指定します。

このオプションの値は、[[トレースセッション] の一覧](trace-session-list.md)の [**新しいファイル**] 列に表示されます。

このオプションは、プロバイダーがトレースログを生成している場合、つまり [**ログセッションオプション**] ページの [[ログトレースイベントデータをファイルに記録する] オプション](basic-trace-session-options.md)を選択した場合にのみ有効です。 このオプションは、循環バッファーまたは[NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)からのログには影響しません。 Windows 2000 ではサポートされていません。

<span id="Use_Global_Sequence_Numbers"></span><span id="use_global_sequence_numbers"></span><span id="USE_GLOBAL_SEQUENCE_NUMBERS"></span>**グローバルシーケンス番号を使用する**  
各トレースメッセージのグローバルシーケンス番号を生成します。

グローバルシーケンス番号は、コンピューター上のすべてのトレースセッションに対して一意です。 このオプションの既定値は**FALSE**です。

このオプションは、Windows 2000 ではサポートされておらず、 [NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)からのログには影響しません。

<span id="Use_Local_Sequence_Number"></span><span id="use_local_sequence_number"></span><span id="USE_LOCAL_SEQUENCE_NUMBER"></span>**ローカルシーケンス番号を使用する**  
各トレースメッセージのローカルシーケンス番号を生成します。 既定値は**TRUE**です。

ローカルシーケンス番号は、トレースセッション内で一意です。

このオプションは、Windows 2000 ではサポートされておらず、 [NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)からのログには影響しません。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**平準**  
トレースプロバイダーの[トレースレベル](trace-level.md)を指定します。 トレースレベルは、プロバイダーが生成するトレースメッセージを決定します。 レベル値の意味は、各プロバイダーによって個別に決定されます。 通常は、増加している詳細レベルを表します。

TraceView がプロバイダーの[トレースメッセージコントロール (tmc) ファイル](trace-message-control-file.md)を見つけることができる場合は、[**トレースフラグとレベルの選択**] ダイアログボックスに表示される一覧からフラグとレベルを選択できます。 [**トレースフラグとレベルの選択**] ダイアログボックスを開くには、[**ログセッションパラメーターのオプション**] ダイアログボックスの [**フラグ**または**レベル**] オプションの**設定**値をクリックします。

トレースレベルの詳細については、Microsoft Windows SDK の**Enabletrace**関数の*EnableLevel*パラメーターの説明を参照してください。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
トレースメッセージを [TraceView] ウィンドウに表示するだけでなく、有効になっているいずれかの方法で、KD または WinDbg にリダイレクトします。 また、このオプションでは、バッファーサイズを、WinDbg で許可されている最大サイズである 3 KB に設定します。 [**バッファーサイズ**] オプションに対して表示される値は無視されます。

デバッガーでトレースメッセージを表示するには、wmitrace と traceprt がホストコンピューター上のデバッガーの検索パスに存在している必要があります。 これらの Dll は、[デバッグツール (Windows の](https://developer.microsoft.com/windows/hardware/)場合) にも含まれています。デバッガーがトレースメッセージの[トレースメッセージ形式 (tmf) ファイル](trace-message-format-file.md)を検索できるようにするには、ホストコンピューター上のデバッガーの検索パスに tmf ファイルが含まれている必要があります。 デバッガーの検索パスを設定するには、wmitrace の searchpath 特殊化されたデバッガー拡張機能を使用するか、% TRACE \_ FORMAT \_ search \_ path% 環境変数の値を設定します。 WinDbg および WMI トレース拡張機能の詳細については、「Windows 用デバッグツール」を参照してください。

<span id="Ignore_TraceView"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**トレースビューを無視する**  
TraceView 操作によって生成されるトレースメッセージを抑制します。

<span id="Virtual_File_Size"></span><span id="virtual_file_size"></span><span id="VIRTUAL_FILE_SIZE"></span>**仮想ファイルのサイズ**  
新しいメッセージ用の領域を確保するために、最も古いメッセージの上書きを開始する前に、TraceView が格納するトレースメッセージの最大数を示します。

値が**0**の場合は、最大値がないことを意味します。 TraceView は、すべてのメッセージを保持し、それらを上書きしません。 このオプションの既定値である**65536**は、ほとんどのシステムで推奨される値です。 大きい値を指定すると、大幅な遅延が発生する可能性があります。

この値は、[トレースセッションの一覧](trace-session-list.md)の [**最大トレースレコード**] 列に表示されます。

 

 





