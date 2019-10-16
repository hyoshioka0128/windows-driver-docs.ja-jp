---
title: XpsAnalyzer のコマンド構文
description: XpsAnalyzer を実行するには、コマンドラインで次の構文とパラメーターを使用してコマンドを入力します。
ms.assetid: f91be3ee-e92a-46c8-ab93-96423a35fd86
keywords:
- XpsAnalyzer コマンド構文ドライバー開発ツール
topic_type:
- apiref
api_name:
- XpsAnalyzer Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 297c48e55ec4921d7d36cabe875e4af7dbe68dbd
ms.sourcegitcommit: 769630c88bf0abd33f702c1eff9336475d92c0d4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72378615"
---
# <a name="xpsanalyzer-command-syntax"></a>XpsAnalyzer のコマンド構文


XpsAnalyzer を実行するには、コマンドラインで次の構文とパラメーターを使用してコマンドを入力します。

```
    XpsAnalyzer [/XpsFile:FileName] [/Directory:DirectoryName] [/FlushSql:SqlFormat]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="________XpsFile_______"></span><span id="________xpsfile_______"></span><span id="________XPSFILE_______"></span> **/XpsFile:**    
分析する XPS ファイルのパスと名前を指定します。

<span id="________Directory_______"></span><span id="________directory_______"></span><span id="________DIRECTORY_______"></span> **/ディレクトリ:**    
1つ以上の XPS ファイルを含むディレクトリへのパスを指定します。

<span id="________FlushSql_______"></span><span id="________flushsql_______"></span><span id="________FLUSHSQL_______"></span> **/Flushsql:**    
XpsAnalyzer ツールを構成して、分析レポートを SQL 形式で作成します。 次の SQL 形式を指定できます。

<span id="SqlServer"></span><span id="sqlserver"></span><span id="SQLSERVER"></span>**SqlServer**  
Microsoft SQL Server と互換性のある形式を指定します。

<span id="MySql"></span><span id="mysql"></span><span id="MYSQL"></span>**MySql**  
MySql オープンソース SQL Server と互換性のある形式を指定します。

<span id="Oracle"></span><span id="oracle"></span><span id="ORACLE"></span>**Oracle11i**  
Oracle SQL Server と互換性のある形式を指定します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

XpsAnalyzer が XML ファイルを分析すると、分析レポートを含む次の2つのファイルが作成されます。

<span id="xpsanalyzer_result.htm_______"></span><span id="XPSANALYZER_RESULT.HTM_______"></span>**XpsAnalyzer\_Result.htm**   
ハイパーテキストマークアップ (HTM) 形式の XPS 分析レポート。

<span id="xpsanalyzer_result.xml_______"></span><span id="XPSANALYZER_RESULT.XML_______"></span>**XpsAnalyzer\_Result.xml**   
XML (拡張マークアップ言語) 形式の XPS 分析レポート。

これらのファイル内では、分析された XPS ファイルの名前の後に分析レポートが続きます。

**/Directory:** 引数が指定されている場合、ファイルには、指定されたディレクトリに存在するすべての XPS ファイルの分析が含まれます。 各ファイルの名前の後に、そのファイルの XPS 分析が続きます。

**/Flushsql:** 引数が指定されている場合、XpsAnalyzer は、XpsAnalyzer\_Result.htm ファイルと XpsAnalyzer\_Result.xml ファイルと共に2つの SQL ファイルを作成します。 SQL ファイルの詳細は次のとおりです。

<span id="setup_sqlserver.sql_______"></span><span id="SETUP_SQLSERVER.SQL_______"></span>**Setup\_SqlServer.sql**   
このファイルには、XPS 分析で検索するために使用できる SQL データベースを準備するためのスクリプトが含まれています。

<span id="update_sqlserver.sql_______"></span><span id="UPDATE_SQLSERVER.SQL_______"></span>**Update\_SqlServer.sql**   
このファイルには、Setup\_SqlServer.sql スクリプトによって作成された SQL データベースに XPS 分析結果を挿入するためのスクリプトが含まれています。

XPS 分析レポートの例については、「 [XpsAnalyzer Output](xpsanalyzer-output.md)」を参照してください。









