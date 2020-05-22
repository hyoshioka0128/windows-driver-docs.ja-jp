---
title: Tracelog
description: Tracelog (Tracelog .exe) は、コマンドプロンプトウィンドウで実行されるイベントトレースコントローラーです。 このセクションでは、Tracelog について説明し、そのコマンド構文について説明し、実際の使用例を示します。
ms.assetid: aa3c144d-260b-44d2-b41c-d18be40ba541
keywords:
- Tracelog WDK
- ソフトウェアトレース WDK、Tracelog
- WDK のトレース、Tracelog
- イベントトレースコントローラー WDK トレースログ
- トレースセッション管理の WDK Tracelog
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c16147dcc2390c6437060a92d692b91fec241f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769566"
---
# <a name="tracelog"></a>Tracelog


Tracelog (Tracelog .exe) は、コマンドプロンプトウィンドウで実行されるイベントトレースコントローラーです。 このセクションでは、Tracelog について説明し、そのコマンド構文について説明し、実際の使用例を示します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tracelog はどこで入手できますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>トレースログ (Tracelog .exe) は、デスクトップアプリの WDK、Visual Studio、および Windows SDK をインストールするときに含まれます。 キットのダウンロードの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Hardware Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows ハードウェアのダウンロード</a>」を参照してください。</p>
<p><strong>Windows Driver Kit (WDK) 8</strong> (インストールパス)</p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> (インストールパス)</p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<div class="alert">
<strong>メモ</strong>   Visual Studio 環境変数% WindowsSdkDir% は、キットがインストールされている Windows kit ディレクトリへのパスを表します。たとえば、C:\Program Files (x86) \Windows Kits\8.1 です。のようになります。
</div>
</td>
</tr>
</tbody>
</table>

 

## <a name="span-idwhat_you_can_do_with_tracelogspanspan-idwhat_you_can_do_with_tracelogspanspan-idwhat_you_can_do_with_tracelogspanwhat-you-can-do-with-tracelog"></a><span id="What_you_can_do_with_Tracelog"></span><span id="what_you_can_do_with_tracelog"></span><span id="WHAT_YOU_CAN_DO_WITH_TRACELOG"></span>Tracelog でできること


イベントトレースコントローラーとして、コマンドプロンプトウィンドウで Tracelog を使用できます。

**メモ**   トレースセッションを制御するには、コンピューターの Performance Log Users グループまたは Administrators グループのメンバーである必要があります (**管理者として実行**)。

Tracelog の機能は次のとおりです。

-   プライベートトレースセッション、 [NT カーネルロガートレースセッション](nt-kernel-logger-trace-session.md)、[グローバルロガートレースセッション](global-logger-trace-session.md)など、[トレースセッション](trace-session.md)を開始または停止します。

-   トレースセッションのプロパティを構成および変更します。

-   [トレースプロバイダー](trace-provider.md)を有効または無効にします

-   トレースセッションバッファーをフラッシュします

-   実行中の (リアルタイムの) トレースセッションを一覧表示します

-   [登録済みのトレースプロバイダー](registered-provider.md)を一覧表示します

-   遅延プロシージャ呼び出し (Dpc) と割り込みサービスルーチン (Isr) に費やされた時間を計測します

Tracelog は、トレースセッション中にプロバイダーによって生成されたトレースメッセージを含むイベントトレースログ (.etl) ファイルを生成します。 メッセージは、ファイルにバイナリ形式で格納されます。 トレースメッセージを読み取り可能な形式で表示するには、 [Traceview](traceview.md)または[tracefmt](tracefmt.md)を使用します。

Tracelog は、カーネルモードおよびプライベート (ユーザーモード) のトレースセッション、および[NT カーネルロガートレース](nt-kernel-logger-trace-session.md)セッションや[グローバルロガートレースセッション](global-logger-trace-session.md)などの特別なセッションを制御します。

Tracelog は、windows 7 以降のバージョンの Windows で実行されます。

Tracelog の機能の多くは、コマンドラインインターフェイスに加えてグラフィカルユーザーインターフェイスを備えた Windows Driver Kit (WDK) に含まれるツールである[Tracelog](traceview.md)でも利用できます。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

-   [**Tracelog のコマンド構文**](tracelog-command-syntax.md)
-   [Tracelog の表示](tracelog-displays.md)
-   [Tracelog の例](tracelog-examples.md)
