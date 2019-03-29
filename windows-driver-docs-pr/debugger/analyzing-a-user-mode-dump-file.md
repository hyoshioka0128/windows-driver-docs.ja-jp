---
title: ユーザーモード ダンプ ファイルの分析
description: ユーザーモード ダンプ ファイルの分析
ms.assetid: b7f3dff8-cd2d-41c9-83ff-f0e5fb2312c0
keywords:
- ダンプ ファイル、ユーザー モード ダンプ ファイルの分析
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: bddd41827cba6ef3e70711b5376c89b14ab17222
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581107"
---
# <a name="analyzing-a-user-mode-dump-file"></a>ユーザーモード ダンプ ファイルの分析

このトピックには次が含まれます。

- [WinDbg をユーザー モード ダンプ ファイルの分析](#windbg)
- [CDB でユーザー モード ダンプ ファイルの分析](#cdb)


## <a name="span-idwindbgspanspan-idwindbgspananalyzing-a-user-mode-dump-file-with-windbg"></a><span id="windbg"></span><span id="WINDBG"></span>WinDbg をユーザー モード ダンプ ファイルの分析


WinDbg では、ユーザー モード メモリ ダンプ ファイルを分析できます。 プロセッサやダンプ ファイルが作成されている Windows バージョンは WinDbg が実行されているプラットフォームを一致させる必要はありません。

### <a name="span-idinstallingsymbolfilesspanspan-idinstallingsymbolfilesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>シンボル ファイルをインストールします。

メモリ ダンプ ファイルを分析する前に、ダンプ ファイルを生成した Windows のバージョンのシンボル ファイルをインストールする必要があります。 これらのファイルは、ダンプ ファイルの分析に使用するデバッガーによって使用されます。 シンボル ファイルの適切なインストールの詳細については、次を参照してください。 [Windows シンボル ファイルのインストール](installing-windows-symbol-files.md)します。

また、いずれかで、システム ダンプ ファイルを生成する原因となった、アプリケーションやシステム サービスのユーザー モード プロセスでは、すべてのシンボル ファイルをインストールする必要があります。 このコードは、ユーザーが記述したが場合、シンボル ファイルする必要がある時に生成されたコードがコンパイルしてリンクします。 商用コードの場合は、製品 CD-ROM のチェックまたはこれらの特定のシンボル ファイルのソフトウェアの製造元にお問い合わせください。

### <a name="span-idstartingwindbgspanspan-idstartingwindbgspanstarting-windbg"></a><span id="starting_windbg"></span><span id="STARTING_WINDBG"></span>WinDbg の開始

ダンプ ファイルを分析するには、WinDbg を開始、 **-z**コマンド ライン オプション。

**windbg -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 オプションの一覧については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

WinDbg が既に実行中、休止モードでは、選択して、クラッシュ ダンプを開くことができます、**ファイル |クラッシュ ダンプを開く**メニュー コマンドまたは CTRL + D ショートカット キーを押します。 ときに、**クラッシュ ダンプを開く**でクラッシュ ダンプ ファイルの名前と完全なパスを入力してください ダイアログ ボックスが表示されたら、**ファイル名**テキスト ボックス、または適切なパスとファイル名を選択するダイアログ ボックスを使用します。 適切なファイルを選択すると、クリックして**オープン**します。

使用して、デバッガーを実行した後も、ダンプ ファイルを開くことができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)とそれに続くコマンド[ **g (移動)** ](g--go-.md).

同時に複数のダンプ ファイルをデバッグすることになります。 これを行う複数を含む **-z** (それぞれが別のファイル名が後に) コマンド ラインでまたはを使用してスイッチ[ **.opendump** ](-opendump--open-dump-file-.md)として追加のダンプ ファイルを追加するにはデバッガーのターゲット。 複数のターゲットのセッションを制御する方法については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

ダンプ ファイルは、一般に、拡張子 .dmp または .mdmp で終了します。 ネットワーク共有または汎用名前付け規則 (UNC) のメモリ ダンプ ファイルの名前のファイルを使用することができます。

ダンプ ファイルを CAB ファイルにパックするための一般的なもできます。 後 (.cab 拡張子を含む)、ファイル名を指定しない場合、 **-z**オプションまたは引数として、 [ **.opendump** ](-opendump--open-dump-file-.md)コマンド、デバッガーは、ダンプ ファイルを読み取ることができますcab ファイルから直接。 ただし、1 つの cab ファイルに格納されている複数のダンプ ファイルがある場合、デバッガーのみうち 1 つを読めるようにします。 デバッガーがシンボル ファイルまたは実行可能ファイルのダンプ ファイルに関連付けられていた場合でも、その他のファイルを cab ファイルから読み取ることは。

### <a name="span-idanalyzingafulluserdumpfilespanspan-idanalyzingafulluserdumpfilespananalyzing-a-full-user-dump-file"></a><span id="analyzing_a_full_user_dump_file"></span><span id="ANALYZING_A_FULL_USER_DUMP_FILE"></span>完全なユーザー ダンプ ファイルの分析

完全なユーザーのダンプ ファイルの分析は、ライブ デバッグ セッションの分析に似ています。 参照してください、[デバッガー コマンド](debugger-commands.md)コマンドはユーザー モード ダンプ ファイルのデバッグに使用できる詳細セクションを参照します。

### <a name="span-idanalyzingminidumpfilesspanspan-idanalyzingminidumpfilesspananalyzing-minidump-files"></a><span id="analyzing_minidump_files"></span><span id="ANALYZING_MINIDUMP_FILES"></span>ミニダンプ ファイルの分析

ユーザー モードのミニダンプ ファイルの分析は、ユーザーの完全なダンプと同じ方法で行われます。 ただし、メモリが保持されているほどためはるかに制限は操作を行うことができます。 ミニダンプ ファイルに保持される情報を超えるメモリにアクセスしようとするコマンドは正しく機能しません。

### <a name="span-idadditionaltechniquesspanspan-idadditionaltechniquesspanadditional-techniques"></a><span id="additional_techniques"></span><span id="ADDITIONAL_TECHNIQUES"></span>その他の方法

ダンプ ファイルから特定の種類の情報の読み取りに使用できる方法では、次を参照してください。[ダンプ ファイルから情報を抽出](extracting-information-from-a-dump-file.md)します。


## <a name="span-idcdbspanspan-idcdbspananalyzing-a-user-mode-dump-file-with-cdb"></a><span id="cdb"></span><span id="CDB"></span>CDB でユーザー モード ダンプ ファイルの分析

ユーザー モード メモリ ダンプ ファイルは、CDB で分析できます。 プロセッサやダンプ ファイルが作成されている Windows バージョンは CDB が実行されているプラットフォームを一致させる必要はありません。

### <a name="span-idinstallingsymbolfilesspanspan-idinstallingsymbolfilesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>シンボル ファイルをインストールします。

メモリ ダンプ ファイルを分析する前に、ダンプ ファイルを生成した Windows のバージョンのシンボル ファイルをインストールする必要があります。 これらのファイルは、ダンプ ファイルの分析に使用するデバッガーによって使用されます。 シンボル ファイルの適切なインストールの詳細については、次を参照してください。 [Windows シンボル ファイルのインストール](installing-windows-symbol-files.md)します。

また、いずれかで、システム ダンプ ファイルを生成する原因となった、アプリケーションやシステム サービスのユーザー モード プロセスでは、すべてのシンボル ファイルをインストールする必要があります。 このコードは、ユーザーが記述したが場合、シンボル ファイルする必要がある時に生成されたコードがコンパイルしてリンクします。 商用コードの場合は、製品 CD-ROM のチェックまたはこれらの特定のシンボル ファイルのソフトウェアの製造元にお問い合わせください。

### <a name="span-idstartingcdbspanspan-idstartingcdbspanstarting-cdb"></a><span id="starting_cdb"></span><span id="STARTING_CDB"></span>開始 CDB

ダンプ ファイルを分析するで CDB を開始、 **-z**コマンド ライン オプション。

**cdb -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 オプションの一覧については、次を参照してください。 [ **CDB コマンド ライン オプション**](cdb-command-line-options.md)します。

使用して、デバッガーを実行した後も、ダンプ ファイルを開くことができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)とそれに続くコマンド[ **g (移動)** ](g--go-.md). これにより、同時に複数のダンプ ファイルをデバッグすることができます。

同時に複数のダンプ ファイルをデバッグすることになります。 これを行う複数を含む **-z** (それぞれが別のファイル名が後に) コマンド ラインでまたはを使用してスイッチ[ **.opendump** ](-opendump--open-dump-file-.md)として追加のダンプ ファイルを追加するにはデバッガーのターゲット。 複数のターゲットのセッションを制御する方法については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

ダンプ ファイルは、一般に、拡張子 .dmp または .mdmp で終了します。 ネットワーク共有または汎用名前付け規則 (UNC) のメモリ ダンプ ファイルの名前のファイルを使用することができます。

ダンプ ファイルを CAB ファイルにパックするための一般的なもできます。 後 (.cab 拡張子を含む)、ファイル名を指定しない場合、 **-z**オプションまたは引数として、 [ **.opendump** ](-opendump--open-dump-file-.md)コマンド、デバッガーは、ダンプ ファイルを読み取ることができますcab ファイルから直接。 ただし、1 つの cab ファイルに格納されている複数のダンプ ファイルがある場合、デバッガーのみうち 1 つを読めるようにします。 デバッガーがシンボル ファイルまたはダンプ ファイルに関連付けられている実行可能ファイルにある場合でも、その他のファイルを cab ファイルから読み取ることが。

### <a name="span-idanalyzingafulluserdumpfilespanspan-idanalyzingafulluserdumpfilespananalyzing-a-full-user-dump-file"></a><span id="analyzing_a_full_user_dump_file"></span><span id="ANALYZING_A_FULL_USER_DUMP_FILE"></span>完全なユーザー ダンプ ファイルの分析

完全なユーザーのダンプ ファイルの分析は、ライブ デバッグ セッションの分析に似ています。 参照してください、[デバッガー コマンド](debugger-commands.md)コマンドはユーザー モード ダンプ ファイルのデバッグに使用できる詳細セクションを参照します。

### <a name="span-idanalyzingminidumpfilesspanspan-idanalyzingminidumpfilesspananalyzing-minidump-files"></a><span id="analyzing_minidump_files"></span><span id="ANALYZING_MINIDUMP_FILES"></span>ミニダンプ ファイルの分析

ユーザー モードのミニダンプ ファイルの分析は、ユーザーの完全なダンプと同じ方法で行われます。 ただし、メモリが保持されているほどためはるかに制限は操作を行うことができます。 ミニダンプ ファイルに保持される情報を超えるメモリにアクセスしようとするコマンドは正しく機能しません。

### <a name="span-idadditionaltechniquesspanspan-idadditionaltechniquesspanadditional-techniques"></a><span id="additional_techniques"></span><span id="ADDITIONAL_TECHNIQUES"></span>その他の方法

ダンプ ファイルから特定の種類の情報の読み取りに使用できる方法では、次を参照してください。[ダンプ ファイルから情報を抽出](extracting-information-from-a-dump-file.md)します。




 

 





