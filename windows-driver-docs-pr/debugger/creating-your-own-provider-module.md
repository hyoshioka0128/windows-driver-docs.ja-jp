---
title: プロバイダー モジュールの作成
description: プロバイダー モジュールの作成
ms.assetid: 4282d375-bcf0-478f-bb2f-a43dc50b09e3
keywords:
- プロバイダーのモジュールのバージョン コントロール システム
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0ce3602ab4c46980e6892efdd539395a45059d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537537"
---
# <a name="creating-your-own-provider-module"></a>プロバイダー モジュールの作成


一般に、プロバイダー モジュールを作成する次の一連のインターフェイスを実装する必要があります。

<span id="_module__SimpleUsage__"></span><span id="_module__simpleusage__"></span><span id="_MODULE__SIMPLEUSAGE__"></span>**$module::SimpleUsage()**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
STDOUT に単純なモジュールの使用状況情報を表示します。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  
なし

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**戻り値**  
なし

<span id="_module__VerboseUsage__"></span><span id="_module__verboseusage__"></span><span id="_MODULE__VERBOSEUSAGE__"></span>**$module::VerboseUsage()**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
STDOUT に詳細なモジュールの使用状況情報を表示します。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  
なし

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**戻り値**  
なし

<span id="_objref____module__new__CommandArguments_"></span><span id="_objref____module__new__commandarguments_"></span><span id="_OBJREF____MODULE__NEW__COMMANDARGUMENTS_"></span>**$objref = $module::new(**<em>@CommandArguments</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
プロバイダーのモジュールのインスタンスを初期化します。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  

<span id="_CommandArguments"></span><span id="_commandarguments"></span><span id="_COMMANDARGUMENTS"></span><em>@CommandArguments</em>  
すべて@ARGVとして一般的な引数: ssindex.cmd によって認識されない引数。

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**戻り値**  
後の操作で使用できる参照。

<span id="_objref-_GatherFileInformation__SourcePath__ServerHashReference_"></span><span id="_objref-_gatherfileinformation__sourcepath__serverhashreference_"></span><span id="_OBJREF-_GATHERFILEINFORMATION__SOURCEPATH__SERVERHASHREFERENCE_"></span>**$objref-&gt;GatherFileInformation(**<em>$SourcePath</em>**,**<em>$ServerHashReference</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
指定されたディレクトリのソースのインデックス処理の必要な情報を収集するモジュールをできるように、 *$SourcePath*パラメーター。 モジュールは、このエントリが各オブジェクト instancebecause の SSIndex が複数回呼び出すさまざまなパスの 1 回だけ呼び出されることを想定しないでください。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  

<span id="_SourcePath"></span><span id="_sourcepath"></span><span id="_SOURCEPATH"></span>*$SourcePath*  
インデックスを作成するソースを含むローカル ディレクトリ。

<span id="_ServerHashReference"></span><span id="_serverhashreference"></span><span id="_SERVERHASHREFERENCE"></span>*$ServerHashReference*  
すべての指定、Srcsrv.ini ファイルからエントリを含むハッシュへの参照。

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**戻り値**  
なし

<span id="__VariableHashReference__FileEntry_____objref-_GetFileInfo__LocalFile_"></span><span id="__variablehashreference__fileentry_____objref-_getfileinfo__localfile_"></span><span id="__VARIABLEHASHREFERENCE__FILEENTRY_____OBJREF-_GETFILEINFO__LOCALFILE_"></span>**(**<em>$VariableHashReference</em>**,**<em>$FileEntry</em>**) = $objref**-&gt;**GetFileInfo(**<em>$LocalFile</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
ソース管理システムから、特定の 1 つのファイルを抽出するために必要な情報を提供します。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  

<span id="_LocalFile"></span><span id="_localfile"></span><span id="_LOCALFILE"></span>*$LocalFile*  
完全修飾ファイル名。

<span id="Return_Values"></span><span id="return_values"></span><span id="RETURN_VALUES"></span>**戻り値**  

<span id="_VariableHashReference"></span><span id="_variablehashreference"></span><span id="_VARIABLEHASHREFERENCE"></span>*$VariableHashReference*  
返されたを解釈するために必要な変数のハッシュ参照 *$FileEntry*します。 Ssindex.cmd では、これらの変数の 1 つのデバッグ ファイル ソース インデックス ストリームに書き込まれる情報の量を削減するために使用するすべてのソース ファイルをキャッシュします。

<span id="_FileEntry"></span><span id="_fileentry"></span><span id="_FILEENTRY"></span>*$FileEntry*  
ソース管理からこのファイルを抽出する SrcSrv を許可するソースのインデックスのストリームに書き込まれるファイルのエントリ。 この行の正確な形式は、ソース管理システムに固有です。

<span id="_TextString___objref-_LongName__"></span><span id="_textstring___objref-_longname__"></span><span id="_TEXTSTRING___OBJREF-_LONGNAME__"></span><em>$TextString</em>**= $objref-&gt;LongName()**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
ユーザーがソース管理システムを識別するために、わかりやすい文字列を提供します。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  
なし

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**戻り値**  

<span id="_TextString"></span><span id="_textstring"></span><span id="_TEXTSTRING"></span>*$TextString*  
ソース管理システムのわかりやすい名前。

<span id="_StreamVariableLines__objref-_SourceStreamVariables__"></span><span id="_streamvariablelines__objref-_sourcestreamvariables__"></span><span id="_STREAMVARIABLELINES__OBJREF-_SOURCESTREAMVARIABLES__"></span><strong>@StreamVariableLines=$objref-&gt;SourceStreamVariables()</strong>  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**目的**  
デバッグ ファイルごとに、ソース ストリームをソース管理に固有の変数を追加するソース管理システムを有効にします。 サンプル モジュールが必要な展開を作成するためこのメソッドを使用して\_CMD と抽出\_ターゲット変数。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**パラメーター**  
なし

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**戻り値**  

<span id="_StreamVariableLines"></span><span id="_streamvariablelines"></span><span id="_STREAMVARIABLELINES"></span><em>@StreamVariableLines</em>  
ソース ストリームの変数のエントリの一覧。

 

 





