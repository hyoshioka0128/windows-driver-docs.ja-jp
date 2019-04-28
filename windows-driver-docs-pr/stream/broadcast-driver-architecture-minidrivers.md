---
title: ブロードキャスト ドライバー アーキテクチャ ミニドライバー
description: ブロードキャスト ドライバー アーキテクチャ ミニドライバー
ms.assetid: 0ad56dbd-6f79-439f-8dfc-8d118d114ddd
keywords:
- ドライバーのアーキテクチャの WDK AVStream、ミニドライバーをブロードキャストします。
- BDA WDK AVStream、ミニドライバー
- ミニドライバー WDK BDA
- BDA ミニドライバー WDK AVStream
- BDA ミニドライバー WDK AVStream、BDA ミニドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66199c036d4c62916810700d4a0e93e3faf43b59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370430"
---
# <a name="broadcast-driver-architecture-minidrivers"></a>ブロードキャスト ドライバー アーキテクチャ ミニドライバー





ドライバーのアーキテクチャ (BDA) のブロードキャストのミニドライバーは、次の操作を実行するハードウェアを制御します。

-   デジタル放送信号のチューニング

-   デジタル信号を demodulating

-   デジタル信号のフレームのキャプチャ

-   シグナルのビデオ、オーディオ、およびデータのストリームに多重化解除

BDA ミニドライバーは AVStream ミニドライバーで実行される、 [AVStream モジュール](avstream-overview.md)カーネル ストリーミング ドライバー *ks.sys*します。 AVStream は、クラスのモデルをストリーミング オーディオとビデオの両方のミニドライバーが統一されたカーネルを提供し、既存のミニドライバー バイナリを変更することがなく COM オブジェクトの使用をサポートするクラス ドライバーです。 AVStream クラス ドライバーは、ほぼ WDM カーネルが準拠しているフィルターをストリームとしてのミニドライバーのフィルターの動作のために必要な既定の動作を提供します。 BDA ミニドライバーの書き込みのタスクを簡素化するには、BDA サポート ライブラリを使用することができます (*Bdasup.lib*) の Microsoft Windows Driver Kit (WDK) に含まれる関数。 このライブラリは、広範な既定の BDA ミニドライバーのプロパティとメソッドのセットの処理を提供します。

通常、ドライバー開発者コードの適切な静的テンプレート構造し BDA サポート ライブラリに登録し、そのすべてのプロパティとメソッドに対する既定の処理を提供するライブラリにあるだけです。 場合によっては、BDA ミニドライバーがプロパティまたはメソッドの要求をインターセプトし、適切な操作を実行する必要があります。

次の図は、BDA ミニドライバーのアーキテクチャの概要を示しています。

![bda ミニドライバーのアーキテクチャの図の概要](images/bdaarch.png)

次のセクションでは、BDA ミニドライバーの実装の詳細について説明しますのいくつかのプロパティとメソッドのセットの詳細を説明しを特定のプロパティとメソッドをインターセプトする方法を示すサンプル コードが含まれています。

[BDA ミニドライバーの初期化](initializing-a-bda-minidriver.md)

[BDA ミニドライバーの開始](starting-a-bda-minidriver.md)

[ディスパッチ テーブルを作成します。](creating-dispatch-tables.md)

[Automation のテーブルを定義します。](defining-automation-tables.md)

[BDA フィルターを初期化しています](initializing-a-bda-filter.md)

[BDA プロパティとメソッドのセットを使用してください。](using-bda-property-and-method-sets.md)

[DirectShow のキャッシュの暗証番号 (pin) 情報](caching-pin-information-for-directshow.md)

[BDA ミニドライバーをセキュリティで保護します。](securing-a-bda-minidriver.md)

[BDA ミニドライバーのフィルターのピンの間の接続](connecting-between-pins-of-filters-for-bda-minidrivers.md)

 

 




