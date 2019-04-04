---
title: WinDbg によるカーネルモード ダンプ ファイルの分析
description: WinDbg によるカーネルモード ダンプ ファイルの分析
ms.assetid: a1493740-5bb5-4335-b177-ee94b93f716b
keywords:
- WinDbg をカーネル モードのダンプ ファイルの分析
- Windbg のカーネル モードのダンプ ファイルを分析、ダンプ ファイルを含む CAB ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c13edb4ef565012cb9e3aadf13242ccbe1d7da6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581149"
---
# <a name="analyzing-a-kernel-mode-dump-file-with-windbg"></a>WinDbg によるカーネルモード ダンプ ファイルの分析


## <span id="ddk_analyzing_a_kernel_mode_dump_file_with_windbg_dbg"></span><span id="DDK_ANALYZING_A_KERNEL_MODE_DUMP_FILE_WITH_WINDBG_DBG"></span>


WinDbg では、カーネル モード メモリ ダンプ ファイルを分析できます。 プロセッサやダンプ ファイルが作成されている Windows バージョンは KD が実行されているプラットフォームを一致させる必要はありません。

### <a name="span-idstartingwindbgspanspan-idstartingwindbgspanstarting-windbg"></a><span id="starting_windbg"></span><span id="STARTING_WINDBG"></span>WinDbg の開始

ダンプ ファイルを分析するには、WinDbg を開始、 **-z**コマンド ライン オプション。

**windbg -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 オプションの一覧については、[ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)を参照してください。

WinDbg が既に実行中、休止モードでは、選択して、クラッシュ ダンプを開くことができます、**ファイル |クラッシュ ダンプを開く**メニュー コマンドまたは CTRL + D ショートカット キーを押します。 ときに、**クラッシュ ダンプを開く**でクラッシュ ダンプ ファイルの名前と完全なパスを入力してください ダイアログ ボックスが表示されたら、**ファイル名**テキスト ボックス、または適切なパスとファイル名を選択するダイアログ ボックスを使用します。 適切なファイルを選択すると、クリックして**オープン**します。

使用して、デバッガーを実行した後も、ダンプ ファイルを開くことができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)とそれに続くコマンド[ **g (移動)** ](g--go-.md).

同時に複数のダンプ ファイルをデバッグすることになります。 これを行う複数を含む **-z** (それぞれが別のファイル名が後に) コマンド ラインでまたはを使用してスイッチ[ **.opendump** ](-opendump--open-dump-file-.md)として追加のダンプ ファイルを追加するにはデバッガーのターゲット。 複数のターゲットのセッションを制御する方法については、[複数のターゲットのデバッグ](debugging-multiple-targets.md)を参照してください。

ダンプ ファイルは、一般に、拡張子 .dmp または .mdmp で終了します。 ネットワーク共有または汎用名前付け規則 (UNC) のメモリ ダンプ ファイルの名前のファイルを使用することができます。

ダンプ ファイルを CAB ファイルにパックするための一般的なもできます。 後 (.cab 拡張子を含む)、ファイル名を指定しない場合、 **-z**オプションまたは引数として、 [ **.opendump** ](-opendump--open-dump-file-.md)コマンド、デバッガーは、ダンプ ファイルを読み取ることができますcab ファイルから直接。 ただし、1 つの cab ファイルに格納されている複数のダンプ ファイルがある場合、デバッガーのみうち 1 つを読めるようにします。 デバッガーがシンボル ファイルまたはダンプ ファイルに関連付けられているその他のファイルがいた場合でも、その他のファイルを CAB から読み取ることが。

### <a name="span-idanalyzingthedumpfilespanspan-idanalyzingthedumpfilespananalyzing-the-dump-file"></a><span id="analyzing_the_dump_file"></span><span id="ANALYZING_THE_DUMP_FILE"></span>ダンプ ファイルの分析

カーネル メモリ ダンプまたは小さいメモリ ダンプを分析する場合は、クラッシュの時点で、メモリに読み込まれている可能性がありますすべての実行可能ファイルをポイントする実行可能イメージのパスを設定する必要があります。

ダンプ ファイルの分析は、ライブ デバッグ セッションの分析に似ています。 参照してください、[デバッガー コマンド](debugger-commands.md)コマンドはカーネル モードでのダンプ ファイルのデバッグに使用できる詳細セクションを参照します。

ほとんどの場合を使用して開始する必要があります[ **! 分析**](-analyze.md)します。 この拡張機能コマンドでは、ダンプ ファイルの自動分析を実行し、多くの有用な情報の多くの場合がします。

[ **.Bugcheck (表示バグ データを確認する)** ](-bugcheck--display-bug-check-data-.md)チェック コードとそのパラメーターは、バグを示しています。 検索では、このバグ チェック、[バグ チェック コード参照](bug-check-code-reference2.md)については、特定のエラー。

次のデバッガー拡張機能は、カーネル モードのクラッシュ ダンプを分析するために特に便利です。

[**! ドライバー**](-drivers.md)

[**!kdext\*.locks**](-locks---kdext--locks-.md)

[**! memusage**](-memusage.md)

[**!vm**](-vm.md)

[**!errlog**](-errlog.md)

[**!process 0 0**](-process.md)

[**!process 0 7**](-process.md)

ダンプ ファイルから特定の種類の情報の読み取りに使用できる方法では、[ダンプ ファイルから情報を抽出](extracting-information-from-a-dump-file.md)を参照してください。

 

 





