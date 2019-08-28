---
title: KD によるカーネルモード ダンプ ファイルの分析
description: KD によるカーネルモード ダンプ ファイルの分析
ms.assetid: 7e8fbf6e-0adc-434c-ba93-f83f49a4af92
keywords:
- KD、ダンプファイルの分析
- ダンプファイルを含む CAB ファイル、KD を使用したカーネルモードダンプファイルの分析
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85017dd657df862c2e745072d837def7b4eb3f1d
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063899"
---
# <a name="analyzing-a-kernel-mode-dump-file-with-kd"></a>KD によるカーネルモード ダンプ ファイルの分析


## <span id="ddk_analyzing_a_kernel_mode_dump_file_with_kd_dbg"></span><span id="DDK_ANALYZING_A_KERNEL_MODE_DUMP_FILE_WITH_KD_DBG"></span>


カーネルモードのメモリダンプファイルは、KD で分析できます。 ダンプファイルが作成されたプロセッサまたは Windows のバージョンは、KD が実行されているプラットフォームと一致する必要はありません。

### <a name="span-idstarting_kdspanspan-idstarting_kdspanstarting-kd"></a><span id="starting_kd"></span><span id="STARTING_KD"></span>KD の開始

ダンプファイルを分析するには、 **-z**コマンドラインオプションを指定して KD を開始します。

**kd -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**オプション (詳細モード) も便利です。 オプションの完全な一覧については、「 [**KD のコマンドラインオプション**](kd-command-line-options.md)」を参照してください。

また、 [**opendump ([ダンプファイルを開く])** ](-opendump--open-dump-file-.md)コマンドを使用し、その後に[**g (enter)** ](g--go-.md)を使用して、デバッガーの実行後にダンプファイルを開くこともできます。

複数のダンプファイルを同時にデバッグすることができます。 これを行うには、コマンドラインに複数**の z**スイッチを含めるか (それぞれに別のファイル名を付ける)、または[ **. opendump**](-opendump--open-dump-file-.md)を使用してデバッガーターゲットとして追加のダンプファイルを追加します。 複数のターゲットセッションを制御する方法の詳細については、「[複数のターゲットのデバッグ](debugging-multiple-targets.md)」を参照してください。

通常、ダンプファイルは拡張子 .dmp または mdmp で終わります。 メモリダンプファイルには、ネットワーク共有または UNC (汎用名前付け規則) ファイル名を使用できます。

また、ダンプファイルが CAB ファイルにパックされることもよくあります。 **-Z**オプションの後にファイル名 (.cab 拡張子を含む) を指定した場合、または[**opendump**](-opendump--open-dump-file-.md)コマンドの引数として指定した場合、デバッガーは、cab から直接、ダンプファイルを読み取ることができます。 ただし、1つの CAB に複数のダンプファイルが格納されている場合、デバッガーはそのうちの1つだけを読み取ることができます。 デバッガーは、シンボルファイルまたはダンプファイルに関連付けられたその他のファイルであっても、CAB から追加ファイルを読み取りません。

### <a name="span-idanalyzing_the_dump_filespanspan-idanalyzing_the_dump_filespananalyzing-the-dump-file"></a><span id="analyzing_the_dump_file"></span><span id="ANALYZING_THE_DUMP_FILE"></span>ダンプファイルの分析

カーネルメモリダンプまたは小さいメモリダンプを分析する場合は、クラッシュ時にメモリに読み込まれた可能性のある実行可能ファイルを指すように、実行可能イメージのパスを設定する必要があります。

ダンプファイルの分析は、ライブデバッグセッションの分析に似ています。 カーネルモードでダンプファイルをデバッグするために使用できるコマンドの詳細については、「[デバッガーコマンド](debugger-commands.md)のリファレンス」セクションを参照してください。

ほとんどの場合、最初に[ **! analyze**](-analyze.md)を使用する必要があります。 この拡張コマンドを実行すると、ダンプファイルの自動分析が実行されるため、多くの場合、有用な情報が得られます。

バグチェックコードとそのパラメーターがバグチェックコードと共に表示され[**ます (バグチェックデータの表示)。** ](-bugcheck--display-bug-check-data-.md) 特定のエラーに関する情報については、[バグチェックコードリファレンス](bug-check-code-reference2.md)でこのバグチェックを参照してください。

次のデバッガー拡張機能は、カーネルモードのクラッシュダンプを分析する場合に特に役立ちます。

[**lm**](lm--list-loaded-modules-.md)

[ **! kdext\*. locks**](-locks---kdext--locks-.md)

[ **! memusage**](-memusage.md)

[ **!vm**](-vm.md)

[ **! errlog**](-errlog.md)

[ **! プロセス 0 0**](-process.md)

[ **! プロセス 0 7**](-process.md)

ダンプファイルから特定の種類の情報を読み取る方法については、「[ダンプファイルからの情報の抽出](extracting-information-from-a-dump-file.md)」を参照してください。

 

 





