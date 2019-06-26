---
title: Tracefmt
description: Tracefmt
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbfd
keywords:
- Tracefmt WDK
- トレースの WDK、Tracefmt ソフトウェア
- トレース メッセージを表示します。
- 書式設定のトレース メッセージを WDK Tracefmt
- トレース メッセージの WDK Tracefmt を書式設定
- ソフトウェアの WDK のトレース、メッセージの書式設定
- トレース WDK、Tracefmt
- トレース メッセージのフォーマット ファイル WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a9ecf7d820cc494d13b75f9dc2e233c0f11f9e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360334"
---
# <a name="tracefmt"></a>Tracefmt


## <span id="ddk_tracefmt_tools"></span><span id="DDK_TRACEFMT_TOOLS"></span>


Tracefmt (Tracefmt.exe) は、書式設定し、イベント トレース ログ ファイル (.etl) またはリアルタイムのトレース セッションからのトレース メッセージを表示します。 コマンド ライン ツールです。 Tracefmt では、コマンド プロンプト ウィンドウで、メッセージを表示したり、テキスト ファイルに保存することができます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tracefmt を見いだすことのできるでしょうか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WDK、Visual Studio、およびデスクトップ アプリ用の Windows SDK をインストールするときに、Tracefmt (Tracefmt.exe) が含まれます。 キットのダウンロード方法の詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows ハードウェア ダウンロード</a>します。</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> (インストール パス)</p>
<p>%WindowsSdkDir%\bin\x64\Tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracefmt.exe</p>
<div class="alert">
<strong>注</strong>  WindowsSdkDir %、Visual Studio 環境変数では、パスを表す Windows キット ディレクトリに、キットがインストールされている、たとえば、C:\Program Files (x86) \windows kits \8.1 です。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

Tracefmt で書式設定命令を使用して、[トレース メッセージの形式 (TMF) ファイル](trace-message-format-file.md)バイナリ トレース メッセージを人間が判読できる形式に変換します。 TMF ファイルまたはトレース プロバイダーのイメージ ファイルを提供し、ある Tracefmt TMF ファイルを作成できます。

によって生成されたトレース イベントの書式を設定できます Tracefmt、 **TraceEvent**関数、およびトレースのメッセージによって生成された、 [ **WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-wmitracemessage)、 **TraceMessage**関数、または[ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロ。 詳細については、 **TraceEvent**と**TraceMessage**関数は、Windows SDK のドキュメントを参照してください。

このセクションの内容:

[Understanding Tracefmt](understanding-tracefmt.md)

[Tracefmt 概念](tracefmt-concepts.md)

[**Tracefmt コマンド**](tracefmt-commands.md)

[Tracefmt 例](tracefmt-examples.md)

 

 





