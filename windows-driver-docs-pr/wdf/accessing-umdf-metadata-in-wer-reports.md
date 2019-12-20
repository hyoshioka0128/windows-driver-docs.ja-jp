---
title: WER レポートでの UMDF メタデータへのアクセス
description: このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) がクラッシュしたときにオペレーティングシステムによって作成される Windows エラー報告 (WER) レポートの場所と内容について説明します。システムは、3つの異なる UMDF イベントの種類 WUDFHostProblem、WUDFUnhandledException、および WUDFVerifierFailure に対して WER レポートを生成します。リフレクターがドライバーホストプロセスを終了するとき、ホストのタイムアウトしきい値を超えたことが原因であることがあります。システムは、WER 情報を含む、wer という名前のファイルを生成します。 具体的には、レポートの wer には、ライブデバッグターゲットにアクセスせずに、UMDF ドライバーをデバッグする場合に役立つ、UMDF メタデータが含まれています。
ms.assetid: ca5fe108-b4fb-4c90-87bc-9901854780d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34a408d946d540a6011e33d0341b92b06b4b0a3c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210232"
---
# <a name="accessing-umdf-metadata-in-wer-reports"></a>WER レポートでの UMDF メタデータへのアクセス


このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) がクラッシュしたときにオペレーティングシステムによって作成される Windows エラー報告 (WER) レポートの場所と内容について説明します。

システムは、 **Wudfhostproblem**、 **WUDFUnhandledException**、および**WUDFVerifierFailure**の3つの異なる UMDF イベントの種類に対して WER レポートを生成します。

リフレクターがドライバーホストプロセスを終了すると、[ホストのタイムアウト](how-umdf-enforces-time-outs.md)しきい値を超えたことが原因で、wer という名前のファイルが生成されます。このファイルには、wer 情報が含まれています。 具体的には、レポートの wer には、ライブデバッグターゲットにアクセスせずに、UMDF ドライバーをデバッグする場合に役立つ、UMDF メタデータが含まれています。

Windows 8.1 では、"C:\\ProgramData\\Microsoft\\Windows\\WER\\ReportQueue ディレクトリにある wer ファイルを見つけることができます。 このディレクトリで、\* フォルダー\_最新の重要ではない\_HostProblem を開き、レポート wer を見つけます。

次の PowerShell コマンドを使用して、UMDF の WER レポートにアクセスすることもできます。

```cpp
get-winevent -providername "Windows Error Reporting" | where-object {$_.Message -like "*wudf*"} | format-list | out-file UmdfReports.txt
```

## <a name="wudfhostproblem-sample-report"></a>WUDFHostProblem のサンプルレポート


**Wudfhostproblem**タイプのサンプルの UMDF WER レポートを次に示します。 これは、上記で説明した ReportQueue ディレクトリから取得されたものです。 PowerShell を使用してレポートを取得する場合、フィールドには、Sig、P1、P2 (Sig\[0\]、Sig\[1\]、Sig\[2\]ではなく、P0、P1、P2 のラベルが付けられます。 それ以外の場合、フィールドは同じであり、同じ値を含んでいます。 このサンプルは、OSR USB FX2 ハードウェアリファレンスボードを使用する WDK サンプルの1つから生成されました。

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

## <a name="wudfhostproblem-fields"></a>WUDFHostProblem のフィールド


次の表は、 **Wudfhostproblem**という種類のレポートのフィールドに使用できる値を示しています。

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
<td align="left"><p>フレームワークによって、この値が<strong>Hostproblem</strong>に設定されます。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">問題</td>
<td align="left"><p>このフィールドには、次のいずれかの値が含まれます。</p>
<ul>
<li>HostFailure</li>
<li>SendFailure</li>
<li>HostTimeout</li>
<li>BadRequest</li>
<li>BadReply</li>
<li>HostFailure</li>
<li>Other</li>
<li>HostDisconnect</li>
<li>最小のハンドル</li>
<li>InvalidInterruptState</li>
<li>IsrTimedOut</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">DetectedBy</td>
<td align="left"><p>次の列挙値のいずれかが含まれています。</p>
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
<td align="left"><p>現在使用されている UMDF ライブラリのバージョンを指定します。 これは、ユーザーがフレームワークライブラリを更新するアクションを実行した場合、オペレーティングシステムに付属していたよりも新しいバージョンである可能性があることに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">ExitCode</td>
<td align="left"><p>次の列挙値のいずれかが含まれています。</p>
<div class="code">
<code>cpp
    WdfHostExit_StillActive = 0x103,
    WdfHostExit_CodeUnknown = 0x70000000,
    WdfHostExit_InternalDriverStopReported,
    WdfHostExit_InternalDriverStopReportFailed,
    WdfHostExit_ExternalTermination</code>
</div>
<p><strong>WdfHostExit_StillActive</strong>は、フレームワークがエラーレポートを作成した時点でホストプロセスが実行されていたことを示します。</p></td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">操作</td>
<td align="left"><p>次の列挙値のいずれかが含まれています。</p>
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
<td align="left">Message</td>
<td align="left"><p>このフィールドの最初の桁は常に1です。これは、IRP が操作に関係していることを示します。 後続の数字のペアは、それぞれ IRP の<strong>MajorFunction</strong>と<strong>minorfunction</strong>を示します。</p>
<p>たとえば、上記のサンプルレポートでは、このフィールドには11b00 という値が含まれています。 これは、この操作は、主な関数値が IRP_MJ_PNP であり、IRP_MN_START_DEVICE のマイナー関数値 (1 = IRP message、1b = IRP_MJ_PNP、00 = IRP_MN_START_DEVICE) で、ドライバーホストプロセスの代わりにリフレクタが処理した IRP であることを意味します。</p></td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">状況</td>
<td align="left"><p>フレームワークは、常にこの値を0xffffffff に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>このフィールドには、問題が発生したドライバーに関連付けられているデバイスのハードウェア ID が含まれます。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfunhandledexception-fields"></a>WUDFUnhandledException のフィールド


次の表では、 **WUDFUnhandledException**型のレポートのフィールドに使用できる値について説明します。

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
<td align="left"><p>この値は、フレームワークによって<strong>UnhandledException</strong>に設定されます。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">Component</td>
<td align="left"><p>このフィールドには、次のいずれかの値が含まれます。</p>
<ul>
<li>ライセンスが無効</li>
<li>プラットフォーム</li>
<li>反射</li>
<li>ドライバーマネージャー</li>
<li>Host</li>
<li>フレームワーク</li>
<li>テスト</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">ExceptionCode</td>
<td align="left"><p>例外が発生した理由。 値の一覧については、「 <a href="https://docs.microsoft.com/windows/win32/api/winnt/ns-winnt-exception_record" data-raw-source="[&lt;strong&gt;EXCEPTION_RECORD&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/winnt/ns-winnt-exception_record)"><strong>EXCEPTION_RECORD</strong></a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">RelativeFaultingAddress</td>
<td align="left"><p>例外が発生したアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">CrashingModuleName</td>
<td align="left">例外を発生させたドライバーの名前。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">CrashingFileVersion</td>
<td align="left">ドライバーのフレームワークバージョン。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">LastDriverName の場合</td>
<td align="left">ドライバースタック内の最初の非 UMDF ドライバーコンポーネントの名前。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">LastDriverVersion</td>
<td align="left">ドライバースタック内の最初の非 UMDF ドライバーコンポーネントのバージョン番号。</td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>現在使用されている UMDF ライブラリのバージョンを指定します。 これは、ユーザーがフレームワークライブラリを更新するアクションを実行した場合、オペレーティングシステムに付属していたよりも新しいバージョンである可能性があることに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left">9</td>
<td align="left">HardwareId</td>
<td align="left"><p>Windows 8 以降では、ハードウェア ID は別のファイルで提供されています。 この場合、フレームワークはこの値を個別に<strong>ダンプ</strong>するように設定します。</p></td>
</tr>
</tbody>
</table>



## <a name="wudfverifierfailure-fields"></a>WUDFVerifierFailure のフィールド


次の表では、 **WUDFVerifierFailure**型のレポートのフィールドに使用できる値について説明します。

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
<td align="left"><p>この値は、フレームワークによって<strong>VerifierFailure</strong>に設定されます。</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">が見つかりません</td>
<td align="left"><p>フレームワークは、この値を<strong>フレームワーク</strong>に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">カテゴリ</td>
<td align="left"><p>このフィールドには、次のいずれかの値が含まれます。</p>
<ul>
<li>内部</li>
<li>[ドライバー]</li>
<li>コール</li>
<li>外部リンク</li>
<li>UnhandledException</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">エラー番号</td>
<td align="left">内部使用のみです。</td>
</tr>
<tr class="odd">
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">位置情報</td>
<td align="left">内部使用のみです。</td>
</tr>
<tr class="even">
<td align="left">5</td>
<td align="left">[ドライバー]</td>
<td align="left">失敗したドライバーモジュールの名前。</td>
</tr>
<tr class="odd">
<td align="left">6</td>
<td align="left">CallerAddress</td>
<td align="left">レポートの生成を開始したルーチンのアドレス。</td>
</tr>
<tr class="even">
<td align="left">7</td>
<td align="left">UMDFVersion</td>
<td align="left"><p>現在使用されている UMDF ライブラリのバージョンを指定します。 これは、ユーザーがフレームワークライブラリを更新するアクションを実行した場合、オペレーティングシステムに付属していたよりも新しいバージョンである可能性があることに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left">8</td>
<td align="left">HardwareId</td>
<td align="left"><p>Windows 8 以降では、ハードウェア ID は別のファイルで提供されています。 この場合、フレームワークはこの値を個別に<strong>ダンプ</strong>するように設定します。</p></td>
</tr>
</tbody>
</table>











