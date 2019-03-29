---
title: WER レポートでの UMDF メタデータへのアクセス
description: このトピックでは、オペレーティング システムがユーザー モード ドライバー フレームワーク (UMDF) がクラッシュしたときに作成した Windows エラー報告 (WER) レポートの内容と場所について説明します。システムは、3 UMDF イベント種類の WUDFHostProblem、WUDFUnhandledException、WER レポートを生成し、WUDFVerifierFailure.When、reflector はもホストのタイムアウトしきい値を超えているため、ドライバーのホスト プロセスを終了します、システムでは、WER の情報を含む、Report.wer という名前のファイルを生成します。 具体的には、Report.wer には、ライブ デバッグ ターゲットへのアクセスなしで UMDF ドライバーをデバッグしようとしている場合に役立つ可能性がある UMDF メタデータが含まれています。
ms.assetid: ca5fe108-b4fb-4c90-87bc-9901854780d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b2832acc46db365c425315e4b92f6dcdd51d6dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579291"
---
# <a name="accessing-umdf-metadata-in-wer-reports"></a>WER レポートでの UMDF メタデータへのアクセス


このトピックでは、オペレーティング システムがユーザー モード ドライバー フレームワーク (UMDF) がクラッシュしたときに作成した Windows エラー報告 (WER) レポートの内容と場所について説明します。

システムでは、WER UMDF イベントの 3 つの異なる種類のレポートが生成されます。**WUDFHostProblem**、 **WUDFUnhandledException**、および**WUDFVerifierFailure**します。

リフレクターが終了したとき、ドライバーのホスト プロセス場合がありますす、[ホスト タイムアウト](how-umdf-enforces-time-outs.md)しきい値を超えている、システムには、WER の情報を含む Report.wer という名前のファイルが生成されます。 具体的には、Report.wer には、ライブ デバッグ ターゲットへのアクセスなしで UMDF ドライバーをデバッグしようとしている場合に役立つ可能性がある UMDF メタデータが含まれています。

Windows 8.1 では、c: Report.wer ファイルを検出できる\\ProgramData\\Microsoft\\Windows\\WER\\ReportQueue ディレクトリ。 このディレクトリに開き、最新の重要でない\_HostProblem\_ \*フォルダー Report.wer を見つけます。

次の PowerShell コマンドを使用して umdf WER レポートを表示できます。

```cpp
get-winevent -providername "Windows Error Reporting" | where-object {$_.Message -like "*wudf*"} | format-list | out-file UmdfReports.txt
```

## <a name="wudfhostproblem-sample-report"></a>WUDFHostProblem サンプル レポート


次にサンプルの種類の UMDF WER レポート**WUDFHostProblem**します。 上記で説明した ReportQueue ディレクトリから取得されています。 フィールドがラベルで Sig ではなく P0、P1、P2 して PowerShell を使用して、レポートを取得する場合\[0\]、Sig\[1\]、Sig\[2\]します。 それ以外の場合、フィールドは同じであり、同じ使用可能な値を含めることができます。 このサンプルは、OSR usb-fx2 のハードウェアの参照をボードを使用するこの WDK サンプルのいずれかから生成されました。

```cpp
Sig[0].Name=EventClass
Sig[0].Value=HostProblem
Sig[1].Name=Problem
Sig[1].Value=HostTimeout
Sig[2].Name=DetectedBy
Sig[2].Value=2
Sig[3].Name=UMDFVersion
Sig[3].Value=6.3.9600
Sig[4].Name=ExitCode
Sig[4].Value=103
Sig[5].Name=Operation
Sig[5].Value=3
Sig[6].Name=Message
Sig[6].Value=11b00
Sig[7].Name=Status
Sig[7].Value=ffffffff
Sig[8].Name=HardwareId
Sig[8].Value=USB\VID_0547&PID_1002&REV_0000
```

## <a name="wudfhostproblem-fields"></a>WUDFHostProblem フィールド


次の表に、可能な型のレポートのフィールド値**WUDFHostProblem します。**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックス</th>
<th align="left">名前</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>フレームワークでは、この値を設定<strong>HostProblem</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">問題</td>
<td align="left"><p>このフィールドには、次の値のいずれかが含まれています。</p>
<ul>
<li>HostFailure</li>
<li>SendFailure</li>
<li>HostTimeout</li>
<li>BadRequest</li>
<li>BadReply</li>
<li>HostFailure</li>
<li>その他</li>
<li>HostDisconnect</li>
<li>LeakedHandle</li>
<li>InvalidInterruptState</li>
<li>IsrTimedOut</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">認識</td>
<td align="left"><p>次の列挙値のいずれかが含まれます。</p>
<div class="code">
<code>cpp
WdfComponentInvalid = 0,
WdfComponentPlatform,
WdfComponentReflector,
WdfComponentDriverManager,
WdfComponentHost,
WdfComponentFramework,
WdfComponentTest,
WdfComponentMax</code>
</div></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>現在使用中の UMDF ライブラリのバージョンを指定します。 も新しいバージョンがありますので注意は、ユーザーは、フレームワーク ライブラリを更新する操作を行った場合、オペレーティング システムに付属します。</p></td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">ExitCode</td>
<td align="left"><p>次の列挙値のいずれかが含まれます。</p>
<div class="code">
<code>cpp
    WdfHostExit_StillActive = 0x103,
    WdfHostExit_CodeUnknown = 0x70000000,
    WdfHostExit_InternalDriverStopReported,
    WdfHostExit_InternalDriverStopReportFailed,
    WdfHostExit_ExternalTermination</code>
</div>
<p><strong>WdfHostExit_StillActive</strong>フレームワーク、エラー レポートの作成時に、ホスト プロセスが実行されていることを示します。</p></td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">操作</td>
<td align="left"><p>次の列挙値のいずれかが含まれます。</p>
<div class="code">
<code>cpp
    WudfOperation_Invalid,
    WudfOperation_Init,
    WudfOperation_HostShutdown,
    WudfOperation_Pnp,
    WudfOperation_Cleanup,
    WudfOperation_Close,
    WudfOperation_Cancel,
    WudfOperation_IO,
    WudfOperation_Interrupt,
    WudfOperation_PoFx,
    WudfOperation_Other,
    WudfOperation_Max</code>
</div></td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">メッセージ</td>
<td align="left"><p>最初の桁は、このフィールドは常に 1 で、操作では IRP が関係していることを示します。 以降の桁の数字のペアを示す、 <strong>MajorFunction</strong>と<strong>MinorFunction</strong>の IRP では、それぞれします。</p>
<p>上記のサンプル レポートで、このフィールドに値 11b00。 つまり、IRP IRP_MJ_PNP の主要な関数の値と IRP_MN_START_DEVICE のマイナー関数値を持つドライバー ホスト プロセスの代わりに、リフレクタ処理したです (1 = IRP メッセージ、1b IRP_MJ_PNP、00 = IRP_MN_START_DEVICE =)。</p></td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">状態</td>
<td align="left"><p>フレームワークは、常にこの値を 0 xffffffff に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>このフィールドには、問題のあるドライバーに関連付けられているデバイスのハードウェア ID が含まれています。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfunhandledexception-fields"></a>WUDFUnhandledException フィールド


次の表に、可能な型のレポートのフィールド値**WUDFUnhandledException**します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックス</th>
<th align="left">名前</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>フレームワークでは、この値を設定<strong>UnhandledException</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">コンポーネント</td>
<td align="left"><p>このフィールドには、次の値のいずれかが含まれています。</p>
<ul>
<li>ライセンスが無効</li>
<li>プラットフォーム</li>
<li>リフレクター</li>
<li>ドライバー マネージャー</li>
<li>Host</li>
<li>Framework</li>
<li>テスト</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">ExceptionCode</td>
<td align="left"><p>理由、例外が発生しました。 値の一覧は、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/desktop/aa363082" data-raw-source="[&lt;strong&gt;EXCEPTION_RECORD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363082)"> <strong>EXCEPTION_RECORD</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">RelativeFaultingAddress</td>
<td align="left"><p>例外が発生したアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">CrashingModuleName</td>
<td align="left">例外が発生したドライバーの名前。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">CrashingFileVersion</td>
<td align="left">ドライバーのフレームワークのバージョン。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">LastDriverName</td>
<td align="left">ドライバー スタックの最初の非 UMDF ドライバー コンポーネントの名前です。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">LastDriverVersion</td>
<td align="left">ドライバー スタックの最初の非 UMDF ドライバー コンポーネントのバージョン番号。</td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>現在使用中の UMDF ライブラリのバージョンを指定します。 も新しいバージョンがありますので注意は、ユーザーは、フレームワーク ライブラリを更新する操作を行った場合、オペレーティング システムに付属します。</p></td>
</tr>
<tr class="even">
<td align="left">9</td>
<td align="left">HardwareId</td>
<td align="left"><p>Windows 8 以降、ハードウェア ID を別のファイルに提供されます。 ここでは、フレームワークがこの値を設定<strong>ダンプとは別に</strong>します。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfverifierfailure-fields"></a>WUDFVerifierFailure フィールド


次の表に、可能な型のレポートのフィールド値**WUDFVerifierFailure**します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックス</th>
<th align="left">名前</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">EventClass</td>
<td align="left"><p>フレームワークでは、この値を設定<strong>VerifierFailure</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">FoundBy</td>
<td align="left"><p>フレームワークでは、この値を設定<strong>Framework</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">カテゴリ</td>
<td align="left"><p>このフィールドには、次の値のいずれかが含まれています。</p>
<ul>
<li>内部</li>
<li>Driver (ドライバー)</li>
<li>呼び出し元</li>
<li>外部リンク</li>
<li>UnhandledException</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">エラー番号</td>
<td align="left">内部でのみ使用します。</td>
</tr>
<tr class="odd">
<td align="left">4</td>
<td align="left">Location</td>
<td align="left">内部でのみ使用します。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">Driver (ドライバー)</td>
<td align="left">失敗したドライバーのモジュールの名前。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">CallerAddress</td>
<td align="left">レポートの生成を開始するルーチンのアドレス。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>現在使用中の UMDF ライブラリのバージョンを指定します。 も新しいバージョンがありますので注意は、ユーザーは、フレームワーク ライブラリを更新する操作を行った場合、オペレーティング システムに付属します。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>Windows 8 以降、ハードウェア ID を別のファイルに提供されます。 ここでは、フレームワークがこの値を設定<strong>ダンプとは別に</strong>します。</p></td>
</tr>
</tbody>
</table>











