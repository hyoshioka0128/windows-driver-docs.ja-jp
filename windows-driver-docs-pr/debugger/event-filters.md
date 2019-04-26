---
title: イベント フィルター
description: イベント フィルター
ms.assetid: 91f2a483-8971-42de-a6c5-cc25409279a5
keywords:
- デバッガー エンジン API、イベント フィルター
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcabc51b5538baa9100e7ddd2e376ab09c1263b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347802"
---
# <a name="event-filters"></a>イベント フィルター


*イベント フィルター*単純なイベントをフィルター処理を提供する。 デバッガー エンジンでのターゲットのイベントの発生後の続行方法が影響を与えます。 イベントの発生時に、エンジンは、そのイベントがイベント フィルターに一致するかどうかを判断します。 場合は、イベント フィルターの中断状態は、ターゲットにデバッガーが中断するかどうかに影響します。 イベントが、例外イベントは、処理の状態は処理またはターゲットでない処理例外を考慮するかどうかを決定します。

**注**  より高度なイベントをフィルター処理する必要がある場合は、イベントのコールバックを使用できます。

 

イベントのフィルターは、次の 3 つのカテゴリに分類されます。

1.  *特定のイベント フィルター*します。 これらは、すべての非例外イベントのフィルターです。 参照してください[**デバッグ\_フィルター\_XXX** ](https://msdn.microsoft.com/library/windows/hardware/ff541490)これらのイベントの一覧についてはします。

2.  *特定の例外フィルター*します。 最初の特定の例外フィルターは、*既定の例外フィルター*します。 残りの部分は、それらの例外をエンジンが組み込みのフィルターのフィルターです。 参照してください[**特定の例外**](https://msdn.microsoft.com/library/windows/hardware/ff558784)特定の例外フィルターの一覧についてはします。

3.  *任意の例外フィルター*します。 これらは、手動で追加された例外イベント フィルターです。

1 と 2 のカテゴリでフィルターと総称されます*特定のフィルター*、2 と 3 のカテゴリでフィルターと総称されますと*例外フィルター*します。 各カテゴリのフィルターの数がによって返される[ **GetNumberEventFilters**](https://msdn.microsoft.com/library/windows/hardware/ff547899)します。

イベントはイベントの種類がフィルターの種類と同じ場合は、特定のイベントのフィルターと一致します。 一部のイベント フィルターは、一致するイベントをさらに制限する追加パラメーターを指定します。

例外イベントでは、例外イベントの例外コードは、例外フィルターの例外コードと同じ場合、例外フィルターが一致します。 例外イベントと同じ例外コードを例外フィルターがない場合は、例外イベントが既定の例外フィルターによって処理されます。

### <a name="span-idcommandsandparametersspanspan-idcommandsandparametersspancommands-and-parameters"></a><span id="commands_and_parameters"></span><span id="COMMANDS_AND_PARAMETERS"></span>コマンドとパラメーター

イベント フィルターには、デバッガー コマンドが関連付けられていることができます。 このコマンドは、フィルターに一致するイベントの発生時にエンジンによって実行されます。 [**GetEventFilterCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff546611)と[ **SetEventFilterCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff556678)を取得し、このコマンドを設定するために使用できます。 例外フィルターの場合は、このコマンドは、例外の初回で実行されます。 次の例外イベント時に、セカンド チャンスに個別のコマンドを実行することができます。 設定するセカンド チャンス コマンドを使用して[ **GetExceptionFilterSecondCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff546653)と[ **SetExceptionSecondChanceCommand**](https://msdn.microsoft.com/library/windows/hardware/ff556687)します。

特定のイベントのフィルターと例外フィルターのパラメーターがによって返される[ **GetSpecificFilterParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff548398)と[ **GetExceptionFilterParameters**](https://msdn.microsoft.com/library/windows/hardware/ff556683). 使用して、中断状態とイベントのフィルター処理の状態を設定できる[ **SetSpecificFilterParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff556795)と**SetExceptionFilterParameters**します。

**SetExceptionFilterParameters**を追加し、任意の例外フィルターを削除できます。

特定のフィルターの簡単な説明がによって返される[ **GetEventFilterText**](https://msdn.microsoft.com/library/windows/hardware/ff546618)します。

一部の特定のフィルターは、フィルターが一致するイベントを制限する引数を受け取ります。 [**GetSpecificFilterArgument** ](https://msdn.microsoft.com/library/windows/hardware/ff548386)と[ **SetSpecificFilterArgument** ](https://msdn.microsoft.com/library/windows/hardware/ff556791)取得され、これらの引数をサポートする特定のフィルターの引数を設定します。 引数、特定のフィルターがない場合は、一致するイベントに制限はありません。 引数とそれらに一致するイベントを制限する方法を取るイベント フィルターを次の表に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">event</th>
<th align="left">条件に一致します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>プロセスを作成します。</p></td>
<td align="left"><p>作成されたプロセスの名前は、argument.1 と一致する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>プロセスを終了します。</p></td>
<td align="left"><p>終了プロセスの名前は、argument.1 と一致する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>モジュールの読み込み</p></td>
<td align="left"><p>読み込まれたモジュールの名前は、argument.1 と一致する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>モジュールのアンロード</p></td>
<td align="left"><p>アンロードされたモジュールのベース アドレスは、argument.2 と同じである必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ターゲットの出力</p></td>
<td align="left"><p>ターゲットからのデバッグ出力は、argument.3 と一致する必要があります。</p></td>
</tr>
</tbody>
</table>

 

**注:**  
1.  引数を使用して、[文字列ワイルドカード構文](string-wildcard-syntax.md)イメージの名前 (パスを無視します) と比較し、イベントの発生時。 モジュールまたはプロセスの名前が使用できない場合は、一致するものと見なされます。

2.  引数では、引数が設定されている場合、エンジンによって評価される式です。

3.  引数を文字列のワイルドカード構文を使用して、ターゲットからのデバッグ出力と比較されます。 出力が不明である場合は、一致するものと見なされます。

 

### <a name="span-idindexandexceptioncodespanspan-idindexandexceptioncodespanindex-and-exception-code"></a><span id="index_and_exception_code"></span><span id="INDEX_AND_EXCEPTION_CODE"></span>インデックスと例外コード

各イベントのフィルターには、インデックスがあります。 インデックスが 0 と 1 つのフィルター (包括) の合計数よりも小さい数値です。 フィルターのカテゴリごとのインデックスの範囲があります、 *SpecificEvents*、 *SpecificExceptions*、および*ArbitraryExceptions* によって返される値[ **GetNumberEventFilters**](https://msdn.microsoft.com/library/windows/hardware/ff547899)、次の表の説明。

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
<th align="left">フィルターの数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>特定のイベント フィルター</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><em>SpecificEvents</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>特定の例外フィルター</p></td>
<td align="left"><p><em>SpecificEvents</em></p></td>
<td align="left"><p><em>SpecificExceptions</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>任意の例外フィルター</p></td>
<td align="left"><p><em>SpecificEvents</em> + <em>SpecificExceptions</em></p></td>
<td align="left"><p><em>ArbitraryExceptions</em></p></td>
</tr>
</tbody>
</table>

 

トピックにある最初のテーブル内の特定のイベント フィルターのインデックスにある[**デバッグ\_フィルター\_XXX**](https://msdn.microsoft.com/library/windows/hardware/ff541490)します。 既定の例外フィルター (最初の特定の例外フィルター) のインデックスが*SpecificEvents*します。 任意の例外フィルターが削除されると、その他の任意の例外フィルターのインデックスを変更できます。

例外フィルターは通常、例外コードを指定します。 ただし、いくつかの方法では、例外のインデックスが必要です。 特定の例外を例外フィルターのインデックスを検索する使用[ **GetExceptionFilterParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff546650)と同じ例外コードを 1 つが表示されるまで、すべての例外フィルターを反復処理する、例外。 特定の例外フィルターの例外コードは、トピックで見つかる[**特定の例外**](https://msdn.microsoft.com/library/windows/hardware/ff558784)します。

### <a name="span-idsystemerrorsspanspan-idsystemerrorsspansystem-errors"></a><span id="system_errors"></span><span id="SYSTEM_ERRORS"></span>システム エラー

システム エラーが発生したときに、エンジンをデバッガーに割り込むまたはまたは指定したレベル以下で、エラーが発生した場合に出力ストリームにエラーを印刷します。 これらのレベルがによって返される[ **GetSystemErrorControl** ](https://msdn.microsoft.com/library/windows/hardware/ff549215)を使用して変更できる[ **SetSystemErrorControl**](https://msdn.microsoft.com/library/windows/hardware/ff556806)します。

 

 





