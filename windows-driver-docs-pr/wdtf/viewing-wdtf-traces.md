---
title: WDTF トレースの有効化と表示
description: WDTF トレースの有効化と表示
ms.assetid: 9bed6042-3691-4a5e-a143-51acf746b1ae
keywords:
- Windows デバイスのテスト フレームワーク WDK、トレース イベント
- WDTF WDK、トレース イベント
- WDK WDTF のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b346e581514c508ca7817b1796c62485c9f95e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573883"
---
# <a name="enabling-and-viewing-wdtf-traces"></a>WDTF トレースの有効化と表示


WDTF*トレース*WDTF オブジェクト内で内部的に発生するイベントのレポートを参照します。 WDTF は大きくインストルメント化されているために、すべての WDTF オブジェクトは、実行中のトレース情報を提供します。 使用してトレースを処理する WDTF [WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)します。 この種類のトレースは、標準化された形式など、WDK のツールを使用して読み取ることができる[traceview で](https://msdn.microsoft.com/library/windows/hardware/ff556063)します。 このトピックでは、使用する方法をについて説明します[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)と[Tracefmt](https://msdn.microsoft.com/library/windows/hardware/ff552974) WDTF ランタイム トレースを表示します。 また、このトピックでは、WDTF トレース レベルをプログラムで構成する方法について説明します。

-   [トレースを収集し、WDTF を保存する方法](#how-to-collect)
-   [WDTF トレースを表示する方法](#how-to-view)
-   [WDTF トレース レベルをプログラムで設定します。](#wdtf-enable-level)

### <a href="" id="how-to-collect"></a>収集および WDTF トレースを保存する方法

**WDTF トレースの収集を開始するには**

1.  テスト コンピューターでは、管理者特権でコマンド プロンプト ウィンドウを開きます (**管理者として実行**) し、次のコマンドを入力します。

    ``` syntax
    logman.exe create trace "autosession\WDTF" -p {6210f559-c7f7-4d2f-b674-4bc9315cecc7} 0xffffffff 0xff -o c:\WDTF_Traces\TraceFile.etl
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v LogFileMode /t REG_DWORD /d 1 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v FileMax /t REG_DWORD /d 16 /f
    reg add HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WDTF /v MaxFileSize /t REG_DWORD /d 0 /f
    ```

2.  コンピューターを再起動します。

参照してください[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332) (Logman.exe) その他のオプションについてはします。 トレースのシーズンを作成する方法の詳細については、次を参照してください。[構成し、自動ロガー セッションを開始する](https://msdn.microsoft.com/library/windows/desktop/aa363687)します。

**WDTF トレースの収集を停止し、ログ ファイルを保存するには**

1.  WDTF トレースの収集を停止し、次のコマンドで、データ コレクターを削除することができます。

    ``` syntax
    logman.exe -stop -ets WDTF
    logman.exe delete "autosession\WDTF"
    ```

2.  コンピューターを再起動します。
3.  テスト コンピューターから別のコンピューターを後で分析するログ ファイルをコピーします。

    収集した ETL ログ ファイルはサイズが非常に大きくすることはできます。 最良の結果をテスト コンピューターからログ ファイルをコピーします (たとえば、c:\\WDTF\_トレース\\TraceFile.etl) 別のコンピューターにします。 テスト コンピューターからログ ファイルを削除できます。

### <a href="" id="how-to-view"></a>WDTF トレースを表示する方法

WDTF トレースを表示するには、ETL ファイルは、書式設定する必要があります。 次の手順の方法を使用して[Tracefmt.exe](https://msdn.microsoft.com/library/windows/hardware/ff552974) ETL ファイルをテキスト ファイルや CSV ファイルに変換します。

**WDTF トレースを表示するには**

1.  たとえば、次のコマンドは c: として保存されている ETL ファイルを変換します。\\WDTF\_トレース\\TraceFile.etl テキスト。

    ``` syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -o OutputTxtFile.txt
    ```

2.  次のコマンドは、c: として保存されている ETL ファイルを変換\\WDTF\_トレース\\TraceFile.etl をコンマ区切りファイル (CSV)。

    ``` syntax
    Tracefmt.exe –r http://msdl.microsoft.com/download/symbols c:\WDTF_Traces\TraceFile.etl -csv –o OutputCsvFile.csv
    ```

3.  Excel のフィルタ リング機能を使用するには、収集されたトレースをフィルター処理するために、Microsoft Excel で CSV ファイルを開きます。 特定の時間をトレースにフィルター選択できます。 特定の WDTF コンポーネントによってログに記録するトレースを調査してトレースをフィルター処理できます。

## <a name="programmatically-configuring-wdtf-trace-levels"></a>WDTF トレース レベルをプログラムで設定します。


すべての WDTF オブジェクトは、実行中にトレース情報を提供します。

WDTF の構成可能なセットを提供する[ **TTraceLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff539616)レベル。 設定する方法については、 **TTraceLevel** 、実行時に特定のオブジェクトのインスタンスの次を参照してください。、 [ **ITracing::SetTraceLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff539522)メソッド。

既定値を設定する方法については[ **TTraceLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff539616)インターフェイスについては、次を参照してください。、 [Windows デバイスのテスト フレームワーク参照](https://msdn.microsoft.com/library/windows/hardware/ff539647)します。

詳細については、それぞれに含まれるトレースの種類の[ **TTraceLevel**](https://msdn.microsoft.com/library/windows/hardware/ff539616)を参照してください、 [ **ITracer** ](https://msdn.microsoft.com/library/windows/hardware/ff539512)インターフェイス。 グローバルにお客様が構成できるこれらのレベルを使用して、 **ITracer**のレジストリ TraceLevel パス。

次の表では、設定できるトレース レベルについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Level</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>オフ:  トレースは提供されません。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>低</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>中です。 このレベルは、既定のトレース レベルです。</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>高</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>完全です。 すべてのトレース情報が報告されます。</p></td>
</tr>
<tr class="even">
<td><p>5-8</p></td>
<td><p>カスタム レベル。</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p>最初のトレース レベルに戻すには、オブジェクトを設定します。</p></td>
</tr>
</tbody>
</table>

 

トレースの内容を使用してデバッグする場合は、トレース レベルをすべてのオブジェクトの 1 に設定され、非常に高い調べているオブジェクトのトレース レベルを検討してください。

トレース レベルの詳細については、次を参照してください。、 [ **ITracer** ](https://msdn.microsoft.com/library/windows/hardware/ff539512)インターフェイス。

## <a name="related-topics"></a>関連トピック
[構成し、自動ロガー セッションを開始します。](https://msdn.microsoft.com/library/windows/desktop/aa363687)  
[Logman](https://go.microsoft.com/fwlink/p/?linkid=136332)  
[Tracefmt](https://msdn.microsoft.com/library/windows/hardware/ff552974)  
[Traceview で](https://msdn.microsoft.com/library/windows/hardware/ff556063)  
[WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)  



