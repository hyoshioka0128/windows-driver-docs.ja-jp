---
title: GPUView の使用
description: GPUView の使用
ms.assetid: 55f589fd-e3ea-4fd2-9e8d-c225c2c3dbb5
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 553d46b0243f59dbe4c59925da179c311360c4e4
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402307"
---
# <a name="using-gpuview"></a>GPUView の使用

GPUView (*GPUView.exe*) は、グラフィックス処理装置 (GPU) と CPU のパフォーマンスを判断するための開発ツールです。 ダイレクトメモリアクセス (DMA) バッファー処理とビデオハードウェア上のその他のすべてのビデオ処理に関して、パフォーマンスが向上します。 GPUView は、Windows Vista の表示ドライバーモデルに準拠したディスプレイドライバーを開発する場合に便利です。 GPUView は、Windows 7 オペレーティングシステムのリリースで導入されました。

GPUView とそれに関連付けられているその他のファイルは、WPT MSI のインストール可能なオプションとして、Windows Performance Toolkit (WPT) に含まれています。 GPUView バイナリは、x86 ベース、x64 ベース、および IA64 ベースのアーキテクチャで使用できます。 たとえば、 *Wpt \_x86.msi*は x86 プラットフォーム用です。 

GPUView は、Windows 7 SDK の一部としてダウンロードすることもできます。 SDK をインストールしたら、C:\Program SDKs\Windows\v7.0\bin にアクセスして、wpt_x64.msi または wpt_x86.msi を実行する必要があります。 これにより、GPUView を含む Windows パフォーマンスツールキットがインストールされます。 

WPT MSI には、次の表で説明するファイルが含まれています。

|ファイル|目的|
|----|----|
|EULA.rtf|法的契約|
|GPUView .chm|GPUView ヘルプファイル|
|Readme.txt|ヘルプファイルに含まれていない追加情報|
|GPUView.exe|ビデオデータを含む ETL ファイルを表示するためのプログラム|
|AEplugin.dll、DWMPlugin.dll、MFPlugin.dll、NTPlugin.dll、DxPlugin.dll、および DxgkPlugin.dll|イベントを解釈するプラグイン|
|CoreTPlugin.dll|統計情報オプションダイアログのプラグイン|
|ログ .cmd|ログ記録に関する適切な情報を有効または無効にするスクリプト|
|SymbolSearchPath.txt|Stackwalk およびその他のイベントを解決するためのシンボルパスを設定するテキストファイル|

GPUView を使用するには、コマンドラインにアクセスし、ログを実行してイベントログを開始します。 次に、再度 .Log を実行して、ログ記録を停止します。 これにより、いくつかの Windows イベントトレーシング () が生成され \* ます。ETL) ファイル。これらのさまざまなストリームはすべて、マージされた .etl と呼ばれる1つのファイルにマージされます。これは GPUView が読み取るものです。 ログに記録されるイベントの例を次に示します。

* スタックトレースおよび切り替えの理由を含む、すべての CPU コンテキストスイッチ。
* すべてのカーネルモードが開始され、スタックトレースが終了します。
* すべてのコマンドバッファーの送信、リソースの作成、破棄、ロック、バインドの各イベントを含む、DirectX グラフィックスカーネルによって記録されたすべての GPU イベント。
* コマンドバッファーの開始時刻や終了時刻、各アダプターの垂直方向の同期間隔など、グラフィックスドライバーによって報告されるイベント。
* ページフォールトなど、パフォーマンスに影響を与える可能性があるその他の多くのシステムイベント。

また、XPerf (同様に Windows SDK の一部である) を使用して ETL ファイルを読み取ることもできます。ただし、GPU 固有のイベントについては理解していません。 これらのログファイルは比較的大きくなる可能性があるため、代わりにコマンドを使用すると、 `Log m` 非常に高い頻度のイベントの多くをスキップできます。

GPUView をダウンロードして使用する方法など、詳細については、「Matthew フィッシャーの[サイト」を](https://graphics.stanford.edu/~mdfisher/GPUView.html)参照してください。このサイトでは、gpuview の作成について説明しています。
