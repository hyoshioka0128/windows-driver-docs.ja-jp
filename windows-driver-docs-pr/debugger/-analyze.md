---
title: 分析
description: 分析の拡張機能では、現在の例外またはバグ チェックに関する情報が表示されます。
ms.assetid: dec760fb-0af6-4504-9855-8fe63c1c9783
keywords:
- Windows デバッグの分析します。
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- analyze
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73f26868420f3cd2a08328fae9117ffaf824d70e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334755"
---
# <a name="analyze"></a>!analyze


**! 分析**拡張機能は、現在の例外またはバグ チェックに関する情報を表示します。

ユーザー モード

```dbgcmd
    !analyze [-v] [-f | -hang] [-D BucketID] 
    !analyze -c [-load KnownIssuesFile | -unload | -help ]
```

カーネル モード

```dbgcmd    
    !analyze [-v] [-f | -hang] [-D BucketID] 
    !analyze -c [-load KnownIssuesFile | -unload | -help ]
    !analyze -show BugCheckCode [BugParameters]
```

## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメーター


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細な出力が表示されます。

<span id="-f"></span><span id="-F"></span>**-f**  
生成、 **! 分析**例外出力します。 このパラメーターを使用して、デバッガーで例外が検出されない場合でも、例外の分析を参照してください。

<span id="-hang"></span><span id="-HANG"></span>**-hang**  
生成 **! 分析**ハングしているアプリケーションの出力。 ターゲットでのバグ チェックや例外が発生しましたが、アプリケーションがハングする理由の分析は、問題に関連性の高い場合は、このパラメーターを使用します。 カーネル モードで **! 分析** **-ハング**システムが保持しているし、DPC キューのチェーンをスキャンし、ロックを調査します。 ユーザー モードで **! 分析** **-ハング**すべてのスレッドが他のスレッドをブロックしているかどうかを判断するスレッドのスタックを分析します。

ユーザー モードでこの拡張機能を実行する前に、応答しなくなった (ハング) する、例外がありますが変更されたため、現在のスレッド別にすると思われるスレッドに、現在のスレッドを変更することを検討します。

<span id="_______-D_______BucketID______"></span><span id="_______-d_______bucketid______"></span><span id="_______-D_______BUCKETID______"></span> **-D** *BucketID*   
関連する指定した項目のみが表示されます*バケット Id*します。

<span id="_______-show_______BugCheckCode___BugParameters_"></span><span id="_______-show_______bugcheckcode___bugparameters_"></span><span id="_______-SHOW_______BUGCHECKCODE___BUGPARAMETERS_"></span> **-表示** *BugCheckCode* \[ *BugParameters*\]  
指定されたバグ チェックに関する情報を表示*BugCheckCode*します。 *BugParameters*バグの 4 つのスペースで区切られたチェック パラメーターに最大を指定します。 これらのパラメーターを使用すると、検索を絞り込むことができます。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
既知の問題を検出すると、デバッガーが実行を継続します。 場合は、問題は、ターゲットに分割、デバッガーは、「既知」の問題ではありません。

使用することができます、 **-c**次サブパラ メーターのオプション。 これらのサブパラ メーターは、既知の問題の一覧を構成します。 実行を単独で発生発生していないします。 実行するまで **! 分析** **-c** **** **-読み込み**少なくとも 1 回、 **! 分析** **-c**効果はありません。

<span id="-load_KnownIssuesFile"></span><span id="-load_knownissuesfile"></span><span id="-LOAD_KNOWNISSUESFILE"></span>**-ロード** *KnownIssuesFile*  
指定した既知の問題のファイルを読み込みます。 *KnownIssuesFile*このファイルのパスとファイル名を指定します。 このファイルは、XML 形式である必要があります。 Sdk のサンプル ファイルを検索できます\\サンプル\\分析\_デバッガーのインストール ディレクトリのサブディレクトリを続行します。 (する必要がありますが実行のデバッグ ツールの Windows がこのファイルの完全インストール)。

既知の問題の一覧、 *KnownIssuesFile*ファイルはすべて、後で、使用 **-c**コマンドを使用するまで **-c** **** **-アンロード**、使用するまで、または **-c** **** **-読み込み**もう一度 (この時点で新しいデータは、古いデータ)。

<span id="-unload"></span><span id="-UNLOAD"></span>**-アンロード**  
現在の既知の問題の一覧をアンロードします。

<span id="-help"></span><span id="-HELP"></span>**-ヘルプ**  
ヘルプを表示、 **! 分析** **-c**コマンド拡張機能の拡張機能、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ユーザー モード例外およびカーネル モードのサンプルの分析の停止エラー (つまり、クラッシュ) と方法の詳細について **! 分析**triage.ini ファイルを使用してを参照してください[を使用して、! 拡張機能を分析](using-the--analyze-extension.md)。

<a name="remarks"></a>注釈
-------

ユーザー モードで **! 分析**現在の例外に関する情報が表示されます。

カーネル モードで **! 分析**最新のバグ チェックに関する情報が表示されます。 バグ チェックが発生した場合、 **! 分析**表示が自動的に生成されます。 使用することができます **! 分析** **-v**追加情報を表示します。 基本的なバグの検査パラメーターのみを表示する場合は、使用、 [ **.bugcheck (表示バグ データを確認する)** ](-bugcheck--display-bug-check-data-.md)コマンド。

ユーザー モード ドライバー フレームワーク (UMDF) 2.15 以降のバージョンを使用するドライバーに対して **! 分析**UMDF 検証エラーと例外に関する情報を提供します。 この機能は、ユーザー モードのメモリ ダンプ ファイルを分析するときに、カーネル モードのライブ デバッグにも実行するときに使用します。 UMDF ドライバー クラッシュが発生した **! 分析**を担当するドライバーを識別します。

 

 





