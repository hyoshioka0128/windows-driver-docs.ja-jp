---
title: Tracepdb
description: Tracepdb
ms.assetid: da7658a8-5fc3-409c-8a34-2aa134b9823b
keywords:
- トレースの WDK、Tracepdb ソフトウェア
- Tracepdb WDK
- TMF ファイル WDK、Tracepdb
- トレース WDK、Tracepdb
- トレース メッセージのフォーマット ファイル WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8715acbeb626c7efb7915aa683902214593b0285
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573234"
---
# <a name="tracepdb"></a>Tracepdb


## <span id="ddk_tracepdb_tools"></span><span id="DDK_TRACEPDB_TOOLS"></span>


Tracepdb (Tracepdb.exe) を作成するコマンド ライン ツールは、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージを抽出することで、フルまたはプライベートからの指示を書式設定[PDB シンボル ファイル](pdb-symbol-files.md)をの[トレース プロバイダー](trace-provider.md) WPP ソフトウェア トレース マクロを使用します。

トレース プロバイダーのプライベート PDB シンボル ファイルを提供できます。 または Tracepdb はディレクトリまたは内部シンボル サーバーを使用して、プロバイダーのプライベート PDB シンボル ファイルを検索できます。 Tracepdb は、Windows 2000 以降のバージョンの Windows で動作します。

**注**  [Tracefmt](tracefmt.md)、し、トレース メッセージを表示します。 ツールは、PDB シンボル ファイルから TMF ファイルを作成もできます。 については、Tracefmt を参照してください。

 

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tracepdb を見いだすことのできるでしょうか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WDK、Visual Studio、およびデスクトップ アプリ用の Windows SDK をインストールするときに、Tracepdb (Tracepdb.exe) が含まれます。 キットのダウンロード方法の詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows ハードウェア ダウンロード</a>を参照してください。</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> (インストール パス)</p>
<p>%WindowsSdkDir%\bin\x64\Tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracepdb.exe</p>
<div class="alert">
<strong>注</strong>  WindowsSdkDir %、Visual Studio 環境変数では、パスを表す Windows キット ディレクトリに、キットがインストールされている、たとえば、C:\Program Files (x86) \windows kits \8.1 です。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

ここでは、次のトピックについて説明します。

[Tracepdb の概要](tracepdb-overview.md)

[**Tracepdb コマンド**](tracepdb-commands.md)
