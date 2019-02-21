---
title: ログの収集と WPP をデコード
description: このトピックでは、収集と、センサー クラスの拡張機能 (CX) のトレース プロバイダー用 Windows ソフトウェア トレース プリプロセッサ (WPP) ログのデコードについて説明します。
ms.assetid: 174CDE37-D0D1-44BF-AD50-5A90C989FDE2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ac909cb176bd644fdaa76895d56ad1c62e3dd014
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553541"
---
# <a name="collecting-and-decoding-wpp-logs"></a>ログの収集と WPP をデコード


このトピックでは、収集と、センサー クラスの拡張機能 (CX) のトレース プロバイダー用 Windows ソフトウェア トレース プリプロセッサ (WPP) ログのデコードについて説明します。

WPP は、トレース プロバイダーと呼ばれるソフトウェア コンポーネントの操作を追跡する方法を提供します。 デコード WPP ログに含まれている PDB ファイルを次に示します。

-   SensorsCx.pdb

-   SensorsUtilsV2.pdb

トレース ログ ツールを使用して、WPP ログを収集します。 詳細については、次を参照してください。 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx)します。 トレースのトレース Guid、トレース フラグ、トレース レベル、または PDB ファイルなどの概念の詳細については、次を参照してください。[トレース ツールの概念](https://msdn.microsoft.com/library/windows/hardware/ff553975.aspx)します。

## <a name="tracing-guid"></a>トレース GUID


次の GUID は、CX ドライバー センサー V2 スタックのトレース プロバイダーを識別します。 この GUID を使用してトレース ログの詳細については、次を参照してください。 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx)します。

``` syntax
c88b592b-6090-480f-a839-ca2434de5844
```

## <a name="trace-flags"></a>トレース フラグ


センサー クラスの拡張機能は、次の WPP を定義します\_コントロール\_GUID トレース フラグ。

``` syntax
EntryExit
DataFlow
Verbose
Information
Warning
Error
Fatal
DriverStatus
```

## <a name="trace-levels"></a>トレース レベル


次のトレース レベルは、トレース ログでの使用状況に対して定義されます。 これらの使用方法の詳細については、次を参照してください。、**レベル**tracelog 構文のパラメーター。

``` syntax
TRACE_LEVEL_FATAL           1
TRACE_LEVEL_ERROR           2
TRACE_LEVEL_WARNING         3
TRACE_LEVEL_INFORMATION     4
TRACE_LEVEL_VERBOSE         5
TRACE_LEVEL_PERF            6
```

## <a name="tracelog-macros"></a>Tracelog マクロ


WPP マクロをその関連するトレース レベルとトレース フラグを次に示します。 メッセージ パラメーターは、printf 関数に対して定義されている標準書式指定文字列です。 パートナーは、書式指定文字列を拡張 WPP も使用できます。 この参照の詳細については、[書式指定文字列を拡張 WPP](https://go.microsoft.com/fwlink/p/?linkid=324276) MSD に関するトピック。 改行文字も記載されて、MSG ので"\\n"は必要ありません。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>マクロ</th>
<th>レベル</th>
<th>Flag</th>
<th>パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TraceFatal</p></td>
<td><p>TRACE_LEVEL_FATAL</p></td>
<td><p>致命的です</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="even">
<td><p>TraceError</p></td>
<td><p>TRACE_LEVEL_ERROR</p></td>
<td><p>エラー</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="odd">
<td><p>TraceWarning</p></td>
<td><p>TRACE_LEVEL_WARNING</p></td>
<td><p>Warning</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="even">
<td><p>TraceInformation</p></td>
<td><p>TRACE_LEVEL_INFORMATION</p></td>
<td><p>情報</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="odd">
<td><p>TraceVerbos</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>Verbose</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="even">
<td><p>TracePerformance</p></td>
<td><p>TRACE_LEVEL_PERF</p></td>
<td><p></p></td>
<td><p>フラグ、メッセージ</p></td>
</tr>
<tr class="odd">
<td><p>TraceData</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>データ フロー</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="even">
<td><p>TraceDriverStatus</p></td>
<td><p>TRACE_LEVEL_INFORMATION</p></td>
<td><p>DriverStatus</p></td>
<td><p>メッセージ</p></td>
</tr>
<tr class="odd">
<td><p>CLX_FunctionEnter</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>CLX_FunctionExit</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>NTSTATUS</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_FunctionEnter</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_FunctionExit</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>NTSTATUS</p></td>
</tr>
</tbody>
</table>

 

## <a name="decoding-etl-logs"></a>ログに記録 ETL のデコード


Tracefmt ツールは、ETL ログのデコードに使用されます。 このツールの詳細については、次を参照してください。 [Tracefmt](https://go.microsoft.com/fwlink/p/?linkid=324212)します。

参照してください、センサー ドライバーのより広範なテストを実行するかどうか [ユニバーサル センサー ドライバーをテストして] (テスト-、-汎用-センサー-driver.md します。

 

 




