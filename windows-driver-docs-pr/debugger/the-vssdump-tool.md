---
title: VSSDump ツール
description: VSSDump ツール
ms.assetid: b213c949-3433-4686-8323-5af83a6ee5b1
keywords:
- SrcSrv、VSSDump ツール
- VSSDump ツール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76c003ba7304593bea2007bcadadbfa4dfe2bfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529892"
---
# <a name="the-vssdump-tool"></a>VSSDump ツール


VSSDump (Vssdump.exe) ツールは、Microsoft Visual SourceSafe のインデックス作成のスクリプトによって使用されます。 インデックスを作成するソース ファイルの一覧を収集します。 このプログラムは、インデックス作成のスクリプトによってファイルが処理されるかを確認するために使用できる貴重なコマンド ライン ユーティリティをもできます。

ソースのインデックス作成の準備をするには、バージョン コントロール サーバーのエントリが含まれるため、Srcsrv.ini を編集します。 これは、この操作を 1 回だけ行う必要があります。 詳細については、サンプル バージョン Srcsrv.ini に表示されます。 環境変数を使用またはインデックス作成のスクリプトをこのファイルの場所を示すために切り替えることができます。 ただし、このファイルの内容は、ビジネスまたは開発システムですべてのプロジェクト全体でグローバルであるため、スクリプトと同じディレクトリに配置することをお勧めします。 このファイルは、別のバージョン コントロール サーバーを一意に識別するために機能します。 提供できるこのファイルの別のバージョンのデバッガーをサーバー上のトラフィックを削減する場合に便利です。 バージョン コントロール サーバーのレプリケート コピーにいるように注意してください。

ソースのインデックス、特定のビルドに確実にソース ファイルがチェックされていないことビルド コンピューター上です。 すべてのファイルはチェック アウトして、編集された場合、それらの変更は最終的なソースのインデックス付きの .pdb ファイルに反映されません。 さらに、ビルド プロセスには、他のファイルからソース ファイルを生成する事前コンパイル パスが含まれている場合は、事前コンパイルの一部としてバージョン管理に生成されたファイルをチェックインする必要があります。

ビルドの完了したら、すべてのソース ファイルと生成される .pdb ファイルのルートにするのには、現在の作業ディレクトリを設定します。 SSIndex を実行します。 パラメーターとして使用しているどのようなバージョン コントロール システムを指定する必要があります。 次に、例を示します。

**ssindex.cmd -server=vss**

SSIndex はどこからでもスクリプトを実行して、ソース ファイルと .pdb ファイルの場所を個別に指定できるようにするパラメーターを受け取ります。 これは、ソースが出力の .pdb ファイルから別の場所に保持される場合に便利です。 次に、例を示します。

**ssindex.cmd -server=vss -source=c:\\**<em>source</em> **-symbols=c:\\**<em>outputdir</em>

これらのディレクトリは、環境変数でも指定できます。 使用して-ですか? または、[概要] タブ 詳細についてはコマンド ライン オプションです。

このスクリプトによって生成された出力の例を次に示します。

```console
## C:\ >ssindex.cmd -system=vss -?

SSIndex.cmd [/option=<value> [...]] [ModuleOptions] [/Debug]
General SrcSrv settings:
     NAME              SWITCH      ENV. VAR        Default
  -----------------------------------------------------------------------------
  1) srcsrv.ini        Ini         SRCSRV_INI      .\srcsrv.ini
  2) Source root       Source      SRCSRV_SOURCE   .
  3) Symbols root      Symbols     SRCSRV_SYMBOLS  .
  4) Control system    System      SRCSRV_SYSTEM   <N/A>
  5) Save File (opt.)  Save        SRCSRV_SAVE     <N/A>
  6) Load File (opt.)  Load        SRCSRV_LOAD     <N/A>
Visual Source Safe specific settings:
     NAME            SWITCH      ENV. VAR        Default
  -----------------------------------------------------------------------------
  A) VSS Server      Server      SSDIR            <N/A>
  B) VSS Client      Client      SSROOT           <Current directory>
  C) VSS Project     Project     SSPROJECT        <N/A>
  D) VSS Label       Label       SSLABEL          <N/A>
Precedence is: Default, environment, cmdline switch. (ie. env overrides default,
switch overrides env).
Using '/debug' will turn on verbose output.
Use "SSIndex.cmd -??" for verbose help information.
## See SrcSrv documentation for more information.
```

バージョン コントロール システムを指定することを回避するために提供されているラッパー スクリプト (Vssindex.cmd) のいずれかを使用できます。 スクリプトのソース インデックスすべての .pdb ファイルは、現在のディレクトリで発見され、すべてのソース ファイルを検索するバージョン管理情報と検出された、現在のディレクトリには以下。 環境変数とコマンド ライン スイッチを使用して、これらのファイルに別の場所を指定できます。

ソースのインデックス作成の完了したら、出力をテストするには、.pdb ファイルに付けて SrcTool を実行します。 このプログラムは、.pdb ファイルがソースのインデックス付きかどうかを示すデータを表示します。 すべてのソース ファイルに固有の情報も表示されます。 最後に、インデックス付きソースの数とのインデックス作成の情報が見つかりませんでしたが、ソースの数が表示されます。 ファイルがソース インデックスが作成されていない場合は-1 %errorlevel% を設定します。 それ以外の場合、%errorlevel% をインデックス付きソース ファイルの数に設定します。

VSSDump できます使用することも個別にソースのインデックス処理中に問題を診断します。 構文は次のとおりです。

**vssdump.exe** *オプション*

*オプション*次のオプションの組み合わせにすることができます。

<span id="-a"></span><span id="-A"></span>**-**  
現在のプロジェクトに制限することではなく、検索結果にすべてのプロジェクトをによりします。 このオプションを使用できません、 **-p**オプション。

<span id="-p_ProjectName"></span><span id="-p_projectname"></span><span id="-P_PROJECTNAME"></span>**-p** *ProjectName*  
により*VSSDump*で指定されたプロジェクトにその検索を制限する*ProjectName*します。 このオプションが存在しない場合は、現在のプロジェクトが使用されます。 このオプションを使用できません、 **-a**オプション。

<span id="-d_RootDirectory"></span><span id="-d_rootdirectory"></span><span id="-D_ROOTDIRECTORY"></span>**-d** *RootDirectory*  
により*VSSDump*で指定したルート ディレクトリにその検索を制限する*RootDirectory*します。 このオプションが存在しない場合は、現在のディレクトリが使用されます。

<span id="-l_Label"></span><span id="-l_label"></span><span id="-L_LABEL"></span>**-l** *ラベル*  
により*VSSDump*によって指定されたラベルの付いたファイルのみを一覧表示する*ラベル*します。

<span id="VSSDump-v_SharePath"></span><span id="vssdump-v_sharepath"></span><span id="VSSDUMP-V_SHAREPATH"></span>*VSSDump * * *-v** *SharePath*  
仮想 SourceSafe データベースの場所があることを示します*SharePath*します。 このオプションは、SSDIR 環境変数で指定されたパスをオーバーライドします。

<span id="-r"></span><span id="-R"></span>**-r**  
により*VSSDump*を再帰的にサブディレクトリを検索します。

<span id="-f"></span><span id="-F"></span>**-f**  
により*VSSDump*ファイル自体をリストすることがなくソース ファイルを含むディレクトリの一覧表示します。

<span id="-i"></span><span id="-I"></span>**-i**  
により*VSSDump*を現在のディレクトリを無視し、プロジェクト全体を一覧表示します。 このオプションを使用できません **-r**します。

<span id="-s"></span><span id="-S"></span>**-s**  
により*VSSDump*スクリプト ファイルで使用するための出力の書式設定します。

<span id="-c"></span><span id="-C"></span>**-c**  
により*VSSDump*仮想 SourceSafe 構成情報のみを表示します。









