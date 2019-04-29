---
title: GPUView の使用
description: GPUView の使用
ms.assetid: 55f589fd-e3ea-4fd2-9e8d-c225c2c3dbb5
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4c4bc466f25c34b2066af7e4f7166469888f385c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389016"
---
# <a name="using-gpuview"></a>GPUView の使用


GPUView (*GPUView.exe*) は、グラフィックス処理装置 (GPU) のパフォーマンスを決定するための開発ツールと CPU。 ダイレクト メモリ アクセス (DMA) バッファーの処理およびビデオ ハードウェアに対して他のすべてのビデオ処理に関して、パフォーマンスに見えます。 GPUView では、Windows Vista のディスプレイ ドライバー モデルに従っているディスプレイ ドライバーの開発に便利です。 GPUView は、Windows 7 オペレーティング システムのリリースで導入されました。

GPUView とそれに関連付けられているその他のファイルは、WPT MSI のインストール可能なオプションとしては Windows パフォーマンス ツールキット (WPT) に含まれます。 GPUView バイナリ x86 ベース、x64 ベース、および IA64 ベースのアーキテクチャを利用できます。 たとえば、 *Wpt\_x86.msi*は、x86 プラットフォーム。 

GPUView、Windows 7 SDK の一部としてダウンロードすることもできます。 SDK をインストールした後は、C:\Program files \microsoft SDKs\Windows\v7.0\bin に移動し、wpt_x64.msi または wpt_x86.msi のいずれかを実行する必要があります。 これにより、GPUView を含む、Windows パフォーマンス ツールキットがインストールされます。 

WPT の MSI には、次の表に記載されているファイルが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ファイル</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>EULA.rtf</em></p></td>
<td align="left"><p>法的契約</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>GPUView.chm</em></p></td>
<td align="left"><p>GPUView ヘルプ ファイル</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Readme.txt</em></p></td>
<td align="left"><p>ヘルプ ファイルに含まれていない追加情報</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>GPUView.exe</em></p></td>
<td align="left"><p>ビデオ データを含む ETL ファイルを表示するためのプログラム</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AEplugin.dll</em>、 <em>DWMPlugin.dll</em>、 <em>MFPlugin.dll</em>、 <em>NTPlugin.dll</em>、 <em>DxPlugin.dll</em>、および<em>DxgkPlugin.dll</em></p></td>
<td align="left"><p>イベントを解釈するプラグイン</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>CoreTPlugin.dll</em></p></td>
<td align="left"><p>統計のオプション ダイアログ ボックス用のプラグイン</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Log.cmd</em></p></td>
<td align="left"><p>オンとオフ、適切な情報のログ記録を有効にするスクリプト</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>SymbolSearchPath.txt</em></p></td>
<td align="left"><p>Stackwalk や他のイベントを解決するのにはシンボル パスを設定するテキスト ファイル</p></td>
</tr>
</tbody>
</table>

GPUView を使用するには、コマンド ラインに移動し、イベントのログ記録を開始する Log.cmd を実行します。 次のログ記録を停止するには、もう一度 Log.cmd を実行します。 いくつか Event Tracing for Windows が生成されます (\*します。ETL) ファイルです。これらのさまざまなストリームのすべてを結合して GPUView の読み取りは 1 つのファイルと呼ばれる Merged.etl にします。 ログに記録されたイベントのいくつかの例は次のとおりです。

* すべて CPU コンテキストの切り替え、スタック トレースなど、切り替えの理由。
* すべてのカーネル モードの出入りおよびスタック トレース。
* すべての GPU イベントすべてのコマンド バッファーの送信やリソースの作成、破棄など、DirectX のグラフィックス カーネルによって記録された、ロック、およびイベントをバインドします。
* コマンド バッファーの開始タグと終了時刻、および各アダプターの垂直方向の同期の間隔など、グラフィックス ドライバーによって報告されたイベント。
* 多くの他のシステム イベント、ページ フォールトなど、パフォーマンスに影響を与えることができます。

ただしそれは理解していない GPU の特定のイベントのいずれか (これは、Windows SDK の一部では同様に) xperf、ETL ファイルを参照することもできます。 これらのログ ファイルは、比較的大きいことができますが、ために、使用できます、`Log m`高周波数のイベントの多くはスキップするコマンドを代わりにします。

詳細については、ダウンロードして GPUView を使用する方法などがあります[ここ](https://graphics.stanford.edu/~mdfisher/GPUView.html)します。 

 

 





