---
title: イベント フィルター
description: イベント フィルター
ms.assetid: 91f2a483-8971-42de-a6c5-cc25409279a5
keywords:
- デバッガーエンジン API, イベントフィルター
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 107d2e88b06fef58bef169b163e7952805c7d686
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837755"
---
# <a name="event-filters"></a>イベント フィルター


*イベントフィルター*は、単純なイベントフィルター処理を提供します。これらは、ターゲットでイベントが発生した後にデバッガーエンジンがどのように処理されるかに影響します。 イベントが発生すると、エンジンは、そのイベントがイベントフィルターと一致するかどうかを判断します。 その場合、イベントフィルターの中断状態は、デバッガーがターゲットに割り込むかどうかに影響します。 イベントが例外イベントの場合、処理の状態によって、例外がターゲットで処理されるかどうかが判断されます。

**メモ**   高度なイベントフィルター処理が必要な場合は、イベントコールバックを使用できます。

 

イベントフィルターは、3つのカテゴリに分類されます。

1.  *特定のイベントフィルター*。 これらは、すべての非例外イベントのフィルターです。 これらのイベントの一覧については、「 [**DEBUG\_FILTER\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx) 」を参照してください。

2.  *特定の例外フィルター*。 最初の特定の例外フィルターは、*既定の例外フィルター*です。 残りの部分は、エンジンに組み込みフィルターがある例外のフィルターです。 特定の例外フィルターの一覧については、「[**特定の例外**](https://docs.microsoft.com/windows-hardware/drivers/debugger/specific-exceptions)」を参照してください。

3.  *任意の例外フィルター*。 これらは、手動で追加された例外イベントのフィルターです。

カテゴリ1および2のフィルターは総称して*特定のフィルター*と呼ばれ、カテゴリ2および3のフィルターは総称して*例外フィルター*と呼ばれます。 各カテゴリのフィルターの数は、 [**Getnumber Eventfilters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbereventfilters)によって返されます。

イベントの種類がフィルターの種類と同じである場合、イベントは特定のイベントフィルターに一致します。 一部のイベントフィルターには、一致するイベントをさらに制限する追加のパラメーターがあります。

例外イベントの例外コードが例外フィルターの例外コードと同じ場合、例外イベントは例外フィルターと一致します。 例外イベントと同じ例外コードを持つ例外フィルターがない場合、例外イベントは既定の例外フィルターによって処理されます。

### <a name="span-idcommands_and_parametersspanspan-idcommands_and_parametersspancommands-and-parameters"></a><span id="commands_and_parameters"></span><span id="COMMANDS_AND_PARAMETERS"></span>コマンドとパラメーター

イベントフィルターには、関連付けられたデバッガーコマンドを含めることができます。 このコマンドは、フィルターに一致するイベントが発生したときにエンジンによって実行されます。 [**Geteventfiltercommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteventfiltercommand)と[**seteventfiltercommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-seteventfiltercommand)を使用して、このコマンドを取得し、設定することができます。 例外フィルターの場合、このコマンドは例外の初回実行時に実行されます。 別のセカンドチャンスコマンドは、2回目の例外イベントに対して実行できます。 2回目のコマンドを取得して設定するには、 [**Getexceptionfiltersecond コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexceptionfiltersecondcommand)と[**Setexceptionsecond chの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexceptionfiltersecondcommand)コマンドを使用します。

特定のイベントフィルターおよび例外フィルターのパラメーターは、 [**Get固有の Filterparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getspecificfilterparameters)および[**getspecificfilterparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexceptionfilterparameters)によって返されます。 イベントフィルターのブレーク状態と処理状態は、 [**Set固有の Filterparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setspecificfilterparameters) **パラメーターと setspecificfilterparameters**を使用して設定できます。

**Setexceptionfilterparameters**を使用して、任意の例外フィルターを追加および削除することもできます。

特定のフィルターについての簡単な説明は、 [**Geteventfiltertext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteventfiltertext)によって返されます。

一部のフィルターは、フィルターが一致するイベントを制限する引数を受け取ります。 [**Get固有の filterargument**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getspecificfilterargument)と[**Set固有の filterargument**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setspecificfilterargument)は、引数をサポートする特定のフィルターの引数を取得して設定します。 特定のフィルターに引数がない場合、一致するイベントに制限はありません。 次の表に、引数を受け取るイベントフィルターと、それらに一致するイベントを制限する方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント</th>
<th align="left">一致条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>プロセスの作成</p></td>
<td align="left"><p>作成されたプロセスの名前は、引数と一致する必要があります。1</p></td>
</tr>
<tr class="even">
<td align="left"><p>プロセスの終了</p></td>
<td align="left"><p>終了したプロセスの名前は、引数と一致する必要があります。1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>モジュールの読み込み</p></td>
<td align="left"><p>読み込まれたモジュールの名前は、引数と一致する必要があります。1</p></td>
</tr>
<tr class="even">
<td align="left"><p>アンロードモジュール</p></td>
<td align="left"><p>アンロードされたモジュールのベースアドレスは、引数と同じである必要があります。2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ターゲットの出力</p></td>
<td align="left"><p>ターゲットからのデバッグ出力は引数と一致する必要があります。3</p></td>
</tr>
</tbody>
</table>

 

**注:**  
1.  引数は文字列の[ワイルドカード構文](string-wildcard-syntax.md)を使用し、イベントが発生すると、イメージ名 (パスを無視します) と比較されます。 モジュールまたはプロセスの名前が使用できない場合は、一致と見なされます。

2.  引数は、引数が設定されたときにエンジンによって評価される式です。

3.  引数は文字列ワイルドカード構文を使用し、ターゲットからのデバッグ出力と比較されます。 出力が不明な場合は、一致と見なされます。

 

### <a name="span-idindex_and_exception_codespanspan-idindex_and_exception_codespanindex-and-exception-code"></a><span id="index_and_exception_code"></span><span id="INDEX_AND_EXCEPTION_CODE"></span>インデックスと例外コード

各イベントフィルターにはインデックスがあります。 インデックスは、0からフィルターの合計数 (包含) までの数値です。 フィルターの各カテゴリのインデックス範囲は、次の表に示すように、 [**Getnumber Eventfilters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbereventfilters)によって返される*固有のイベント*、*固有の例外*、および*ArbitraryExceptions*の値から見つけることができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント フィルター</th>
<th align="left">最初のフィルターのインデックス</th>
<th align="left">フィルター数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>特定のイベントフィルター</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><em>固有のイベント</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>特定の例外フィルター</p></td>
<td align="left"><p><em>固有のイベント</em></p></td>
<td align="left"><p><em>固有の例外</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>任意の例外フィルター</p></td>
<td align="left"><p>固有の<em>イベント</em>の+ <em>例外</em></p></td>
<td align="left"><p><em>ArbitraryExceptions</em></p></td>
</tr>
</tbody>
</table>

 

特定のイベントフィルターのインデックスは、「 [**DEBUG\_FILTER\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx)」に記載されている最初のテーブルにあります。 既定の例外フィルターのインデックス (最初の特定の例外フィルター) は、固有の*イベント*です。 任意の例外フィルターが削除されると、他の任意の例外フィルターのインデックスが変更される可能性があります。

例外フィルターは、通常、例外コードによって指定されます。 ただし、一部のメソッドでは、例外のインデックスが必要です。 特定の例外に対する例外フィルターのインデックスを検索するには、 [**Getexceptionfilterparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexceptionfilterparameters)を使用して、例外と同じ例外コードを持つ例外フィルターを検索します。 特定の例外フィルターの例外コードについては、トピック「[**特定の例外**](https://docs.microsoft.com/windows-hardware/drivers/debugger/specific-exceptions)」を参照してください。

### <a name="span-idsystem_errorsspanspan-idsystem_errorsspansystem-errors"></a><span id="system_errors"></span><span id="SYSTEM_ERRORS"></span>システムエラー

システムエラーが発生すると、エンジンはデバッガーを中断するか、指定されたレベル以下でエラーが発生した場合にエラーを出力ストリームに出力します。 これらのレベルは[**GetSystemErrorControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getsystemerrorcontrol)によって返され、 [**Setsystemerrorcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setsystemerrorcontrol)を使用して変更できます。

 

 





