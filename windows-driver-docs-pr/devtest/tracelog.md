---
title: Tracelog
description: トレース ログ (Tracelog.exe) は、コマンド プロンプト ウィンドウで実行されているイベント トレース コント ローラーです。 ここでは、トレース ログについて説明します、そのコマンドの構文について説明しに使用するための実用的な例を示します。
ms.assetid: aa3c144d-260b-44d2-b41c-d18be40ba541
keywords:
- Tracelog WDK
- ソフトウェアの WDK、トレース ログのトレース
- WDK、トレース ログのトレース
- WDK のトレース ログをコント ローラー イベントのトレース
- WDK のトレース ログ トレース セッションの管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1505480232f53ad163fb5204c5d0375a8e0f0ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369716"
---
# <a name="tracelog"></a>Tracelog


トレース ログ (Tracelog.exe) は、コマンド プロンプト ウィンドウで実行されているイベント トレース コント ローラーです。 ここでは、トレース ログについて説明します、そのコマンドの構文について説明しに使用するための実用的な例を示します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トレース ログはどこで入手できますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WDK、Visual Studio、およびデスクトップ アプリ用の Windows SDK をインストールするときに、トレース ログ (Tracelog.exe) が含まれます。 キットのダウンロード方法の詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows ハードウェア ダウンロード</a>します。</p>
<p><strong>Windows Driver Kit (WDK) 8</strong> (インストール パス)</p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> (インストール パス)</p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<div class="alert">
<strong>注</strong>  WindowsSdkDir %、Visual Studio 環境変数では、パスを表す Windows キット ディレクトリに、キットがインストールされている、たとえば、C:\Program Files (x86) \windows kits \8.1 です。
</div>
</td>
</tr>
</tbody>
</table>

 

## <a name="span-idwhatyoucandowithtracelogspanspan-idwhatyoucandowithtracelogspanspan-idwhatyoucandowithtracelogspanwhat-you-can-do-with-tracelog"></a><span id="What_you_can_do_with_Tracelog"></span><span id="what_you_can_do_with_tracelog"></span><span id="WHAT_YOU_CAN_DO_WITH_TRACELOG"></span>トレース ログで行うことができます。


トレース ログは、イベント トレースのコント ローラーとしてコマンド プロンプト ウィンドウで使用できます。

**注**  トレース セッションを制御するには、Performance Log Users グループまたはコンピューターの Administrators グループのメンバーである (**管理者として実行**)。

トレース ログの機能は次のとおりです。

-   開始し、停止を[トレース セッション](trace-session.md)、プライベートのトレース セッションを含む[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)、および[グローバル ロガー トレース セッション](global-logger-trace-session.md)

-   構成し、トレース セッションのプロパティを変更

-   無効にでき[トレース プロバイダー](trace-provider.md)

-   フラッシュ トレース セッション バッファー

-   (リアルタイム) のトレース セッションを実行しているリスト

-   一覧表示[トレース プロバイダーの登録](registered-provider.md)

-   遅延プロシージャに費やされた時間を計測呼び出し (Dpc) および割り込みサービス ルーチン (Isr)

トレース ログは、トレース セッション中に、プロバイダーによって生成されたトレース メッセージを含むイベント トレース ログ (.etl) ファイルを生成します。 メッセージは、バイナリ形式のファイルに格納されます。 読みやすい形式で、トレース メッセージを表示する使用[traceview で](traceview.md)または[Tracefmt](tracefmt.md)します。

トレース ログなどのコントロールのカーネル モードとプライベート (ユーザー モード) トレース セッション、および特殊なセッション、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)と[グローバル ロガー トレース セッション](global-logger-trace-session.md)します。

トレース ログは、Windows 7 以降のバージョンの Windows で動作します。

使用可能なトレース ログの機能の多くはも[traceview で](traceview.md)、コマンド ライン インターフェイスだけでなくグラフィカル ユーザー インターフェイスを持つ Windows Driver Kit (WDK) で含まれているツールです。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

-   [**Tracelog コマンドの構文**](tracelog-command-syntax.md)
-   [トレース ログが表示されます。](tracelog-displays.md)
-   [トレース ログの例](tracelog-examples.md)
