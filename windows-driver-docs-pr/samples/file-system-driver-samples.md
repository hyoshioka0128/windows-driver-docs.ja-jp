---
title: ファイル システム ドライバーのサンプル
description: このディレクトリのドライバーサンプルは、デバイスのカスタムファイルシステムドライバーを作成するための開始点となります。
ms.assetid: 9F2F995E-EA20-4877-B96C-5FF082CE886D
ms.date: 11/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: ec42afa31f558dc36c5d8bb100bdb4b858c1fe8b
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735242"
---
# <a name="file-system-driver-samples"></a>ファイル システム ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタムファイルシステムドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [CDFS ファイルシステムドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cdfs-file-system-driver) | CD-ROM ファイルシステムドライバー (cdfs) サンプルは、リムーバブルメディア用のファイルシステムドライバーです。 |
| [fastfat ファイルシステムドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/fastfat-file-system-driver) | 新しいファイルシステムのモデルとして使用される Windows inbox FastFAT ファイルシステムに基づくファイルシステムドライバー。 |
| [AvScan ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avscan-file-system-minifilter-driver) | このフィルターは、ファイル内のデータを検査するトランザクション対応のファイルスキャナーです。 ウイルス対策は、この方法で動作する可能性があります。 |
| [CancelSafe ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cancelsafe-file-system-minifilter-driver) | キャンセルセーフキューの使用方法を示すミニフィルター。 |
| [CDO ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cdo-file-system-minifilter-driver) | フィルターを使用してコントロールデバイスオブジェクト (CDO) を使用する例を次に示します。 |
| [ファイルシステムミニフィルタードライバーの変更](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/change-file-system-minifilter-driver) | リアルタイムでファイルの変更を監視するトランザクション対応フィルター。 |
| [Ctx ファイルシステムミニフィルタードライブ](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ctx-file-system-minifilter-drive) | ミニフィルターでインスタンス、ファイル、ストリーム、およびストリームハンドルにコンテキストをアタッチする方法を示します。 |
| [ファイルシステムミニフィルタードライバーの削除](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/delete-file-system-minifilter-driver) | ファイルまたはストリームの削除を検出する方法を示します。 |
[メタデータマネージャーファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/metadata-manager-file-system-minifilter-driver) | ミニフィルターに対応するメタデータを格納するためにファイルを使用する方法の例として機能します。 このサンプルの実装では、ファイルに対する変更をブロックする必要がある場合や、ファイルを一時的に閉じる場合にミニフィルターが必要になることがあります。 |
| [Minispy ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/minispy-file-system-minifilter-driver) | システムで発生した i/o とトランザクションのアクティビティを監視してログに記録するツール。 |
| [NameChanger ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/namechanger-file-system-minifilter-driver) | マッピングを使用して、ボリュームの名前空間のある部分から別のパートにディレクトリを Grafts します。 ミニフィルターでは、名前プロバイダーとして機能し、ディレクトリの列挙にエントリを挿入し、ディレクトリの変更通知を転送することで、この錯覚を維持します。 |
| [NullFilter ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/nullfilter-file-system-minifilter-driver) | フィルタマネージャへの登録を示すミニフィルター。 |
| [パススルーファイルシステムミニフィルタードライバー](h https://docs.microsoft.com/samples/microsoft/windows-driver-samples/passthrough-file-system-minifilter-driver) | さまざまな種類の i/o 要求に対してコールバック関数を指定する方法を示します。 |
| [スキャナーファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/scanner-file-system-minifilter-driver) | ファイルデータスキャナーの例。 通常、ウイルス対策フィルターの種類は次のとおりです。 |
| [簡略化されたファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/simrep-file-system-minifilter-driver) | ファイルシステムフィルターを使用してファイルシステムの再解析ポイント動作をシミュレートし、ファイルを別のパスに開く方法を示します。 |
[スワップバッファーファイルシステムミニフィルタードライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/swapbuffer-file-system-minifilter-driver) | データの読み取りと書き込みの間でバッファーを切り替える方法について説明します。 この手法は、暗号化フィルターに特に役立ちます。 |
