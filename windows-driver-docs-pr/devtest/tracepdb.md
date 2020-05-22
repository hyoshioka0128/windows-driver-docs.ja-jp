---
title: Tracepdb
description: Tracepdb
ms.assetid: da7658a8-5fc3-409c-8a34-2aa134b9823b
keywords:
- ソフトウェアトレース WDK、Tracepdb
- Tracepdb WDK
- TMF ファイル WDK、Tracepdb
- WDK のトレース、Tracepdb
- トレースメッセージフォーマットファイル WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d559734dd426890d3e88abdeb3d192dc3ba62f0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769448"
---
# <a name="tracepdb"></a>Tracepdb


## <span id="ddk_tracepdb_tools"></span><span id="DDK_TRACEPDB_TOOLS"></span>


Tracepdb (Tracepdb) は、コマンドラインツールです。このツールは、WPP ソフトウェアトレースマクロを使用する[トレースプロバイダー](trace-provider.md)の完全またはプライベートの[PDB シンボルファイル](pdb-symbol-files.md)からトレースメッセージの書式設定命令を抽出することによって、トレースメッセージ[形式 (tmf) ファイル](trace-message-format-file.md)を作成します。

トレースプロバイダーまたは Tracepdb のプライベート PDB シンボルファイルを指定すると、ディレクトリまたは内部シンボルサーバーを使用して、プロバイダーのプライベート PDB シンボルファイルを見つけることができます。 Tracepdb は、Windows 2000 以降のバージョンの Windows で実行されます。

**注**トレースメッセージを書式設定して表示するためのツールである  [TRACEFMT](tracefmt.md)は、PDB シンボルファイルから tmf ファイルを作成することもできます。 詳細については、「Tracefmt」を参照してください。

 

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tracepdb はどこで入手できますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Tracepdb (Tracepdb .exe) は、デスクトップアプリの WDK、Visual Studio、および Windows SDK をインストールするときに含まれます。 キットのダウンロードの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Hardware Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows ハードウェアのダウンロード</a>」を参照してください。</p>
<p><strong>Windows Driver Kit (WDK) 8.1</strong> (インストールパス)</p>
<p>%WindowsSdkDir%\bin\x64\Tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\Tracepdb.exe</p>
<div class="alert">
<strong>メモ</strong>   Visual Studio 環境変数% WindowsSdkDir% は、キットがインストールされている Windows kit ディレクトリへのパスを表します。たとえば、C:\Program Files (x86) \Windows Kits\8.1 です。のようになります。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

ここでは、次のトピックについて説明します。

[Tracepdb の概要](tracepdb-overview.md)

[**Tracepdb のコマンド**](tracepdb-commands.md)
