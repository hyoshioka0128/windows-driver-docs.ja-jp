---
title: Tracefmt
description: Tracefmt
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbfd
keywords:
- Tracefmt WDK
- ソフトウェアトレース WDK、Tracefmt
- トレースメッセージの表示
- トレースメッセージの書式設定 WDK Tracefmt
- トレースメッセージのフォーマット (WDK Tracefmt)
- ソフトウェアトレース WDK, 書式設定メッセージ
- WDK のトレース、Tracefmt
- トレースメッセージフォーマットファイル WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d06f7347e233e2a2dc17f162c1c98e6135bcdd69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839265"
---
# <a name="tracefmt"></a>Tracefmt


## <span id="ddk_tracefmt_tools"></span><span id="DDK_TRACEFMT_TOOLS"></span>


Tracefmt (Tracefmt .exe) は、イベントトレースログファイル (.etl) またはリアルタイムトレースセッションからのトレースメッセージを書式設定して表示するコマンドラインツールです。 Tracefmt は、コマンドプロンプトウィンドウでメッセージを表示したり、テキストファイルに保存したりできます。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tracefmt はどこで入手できますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Tracefmt (Tracefmt) は、デスクトップアプリの WDK、Visual Studio、および Windows SDK をインストールするときに含まれます。 キットのダウンロードの詳細については、「 <a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows ハードウェアのダウンロード</a>」を参照してください。</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> (インストールパス)</p>
<p>%WindowsSdkDir%\bin\x64\Tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracefmt.exe</p>
<div class="alert">
<strong>注</strong>  Visual Studio 環境変数% WindowsSdkDir% は、キットがインストールされている Windows kit ディレクトリへのパスを表します。たとえば、C:\Program files (x86) \windows kits\8.1 です。のようになります。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

Tracefmt は、[トレースメッセージ形式 (TMF) ファイル](trace-message-format-file.md)の書式設定命令を使用して、バイナリトレースメッセージを人間が判読できる形式に変換します。 TMF ファイルを指定するか、トレースプロバイダーのイメージファイルを指定して、Tracefmt で TMF ファイルを作成することができます。

Tracefmt は、 **Traceevent**関数によって生成されたトレースイベントと、 [**WmiTraceMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-wmitracemessage)、 **TraceMessage**関数、または[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロによって生成されたトレースメッセージを書式設定できます。 **Traceevent**関数と**TraceMessage**関数の詳細については、Windows SDK のドキュメントを参照してください。

このセクションの内容は次のとおりです。

[Tracefmt について](understanding-tracefmt.md)

[Tracefmt の概念](tracefmt-concepts.md)

[**Tracefmt コマンド**](tracefmt-commands.md)

[Tracefmt の例](tracefmt-examples.md)

 

 





