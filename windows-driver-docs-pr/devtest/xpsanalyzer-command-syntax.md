---
title: XpsAnalyzer コマンドの構文
description: XpsAnalyzer を実行するには、次の構文とパラメーターを使用してコマンドラインでコマンドを入力します。
ms.assetid: f91be3ee-e92a-46c8-ab93-96423a35fd86
keywords:
- XpsAnalyzer コマンド構文のドライバーの開発ツール
topic_type:
- apiref
api_name:
- XpsAnalyzer Command Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2bab8bdba1fdd7cfb202b6f93514e83625fe36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538913"
---
# <a name="xpsanalyzer-command-syntax"></a>XpsAnalyzer コマンドの構文


XpsAnalyzer を実行するには、次の構文とパラメーターを使用してコマンドラインでコマンドを入力します。

```
    XpsAnalyzer [/XpsFile:FileName] [/Directory:DirectoryName] [/FlushSql:SqlFormat]] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________XpsFile_______"></span><span id="________xpsfile_______"></span><span id="________XPSFILE_______"></span> **/XpsFile:**   
分析する XPS ファイルの名前とパスを指定します。

<span id="________Directory_______"></span><span id="________directory_______"></span><span id="________DIRECTORY_______"></span> **/Directory:**   
1 つまたは複数の XPS ファイルを含むディレクトリへのパスを指定します。

<span id="________FlushSql_______"></span><span id="________flushsql_______"></span><span id="________FLUSHSQL_______"></span> **/FlushSql:**   
SQL 形式で、分析レポートを作成する XpsAnalyzer ツールを構成します。 次のような SQL 形式を指定できます。

<span id="SqlServer"></span><span id="sqlserver"></span><span id="SQLSERVER"></span>**Sql Server**  
Microsoft SQL Server と互換性のある形式を指定します。

<span id="MySql"></span><span id="mysql"></span><span id="MYSQL"></span>**MySql**  
MySql のオープン ソースの SQL Server と互換性のある形式を指定します。

<span id="Oracle"></span><span id="oracle"></span><span id="ORACLE"></span>**Oracle**  
Oracle の SQL Server と互換性のある形式を指定します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

XpsAnalyzer は、XML ファイルを分析し、分析レポートが含まれている次の 2 つのファイルが作成されます。

<span id="xpsanalyzer_result.htm_______"></span><span id="XPSANALYZER_RESULT.HTM_______"></span>**XpsAnalyzer\_Result.htm**   
ハイパー テキスト マークアップ (HTM) 形式で XPS 分析レポートです。

<span id="xpsanalyzer_result.xml_______"></span><span id="XPSANALYZER_RESULT.XML_______"></span>**XpsAnalyzer\_Result.xml**   
EXtensible Markup Language (XML) 形式で XPS 分析レポートです。

これらのファイル内でが分析されて XPS ファイルの名前が続きます分析レポート。

場合、 **/ディレクトリ:** 引数を指定すると、ファイルには、指定されたディレクトリ内にあるすべての XPS ファイルの分析が含まれています。 各ファイルの名前には、そのファイルの分析を XPS が続きます。

場合、 **/FlushSql:** 引数を指定すると、XpsAnalyzer、XpsAnalyzer と共に 2 つの SQL ファイルを作成します\_Result.htm と XpsAnalyzer\_Result.xml ファイル。 SQL ファイルの詳細については、folllows としては。

<span id="setup_sqlserver.sql_______"></span><span id="SETUP_SQLSERVER.SQL_______"></span>**Setup\_SqlServer.sql**   
このファイルには、XPS 分析に検索に使用できる SQL データベースを準備するためのスクリプトが含まれています。

<span id="update_sqlserver.sql_______"></span><span id="UPDATE_SQLSERVER.SQL_______"></span>**Update\_SqlServer.sql**   
このファイルには、設定を使用して作成した SQL database に XPS 分析の結果を挿入するスクリプトが含まれています。\_SqlServer.sql スクリプト。

XPS の分析レポートの例は、[XpsAnalyzer 出力](xpsanalyzer-output.md)を参照してください。









