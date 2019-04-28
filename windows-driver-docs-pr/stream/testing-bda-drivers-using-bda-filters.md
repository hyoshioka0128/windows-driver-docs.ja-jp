---
title: BDA フィルターを使用した BDA ドライバーのテスト
description: BDA フィルターを使用した BDA ドライバーのテスト
ms.assetid: 136810b7-9378-482b-8e21-a7eae0142909
keywords:
- ドライバーをテスト ドライバーのアーキテクチャの WDK AVStream をブロードキャストします。
- BDA WDK AVStream、ドライバーのテスト
- ドライバー WDK、BDA のテスト
- DirectShow フィルター WDK AVStream
- グラフ エディターの WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2a9dec9af2e17292f22cb8ab242bc95c6c3c579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364802"
---
# <a name="testing-bda-drivers-using-bda-filters"></a>BDA フィルターを使用した BDA ドライバーのテスト





DirectShow フィルター グラフ エディターを使用することができます (*Graphedt.exe*) コンポーネントをテストすることができるように、フィルターのグラフで BDA コンポーネントの DirectShow フィルター インスタンスを挿入します。 グラフ エディターには、Microsoft Windows Driver Kit (WDK) から入手できます。

グラフ内のフィルターの種類の他のピンをコンポーネントのフィルターのインスタンスによって公開されているピンを接続するよう、BDA コンポーネントの基本的なテストを実行するのに、グラフ エディターを使用することができます。

グラフ エディターを使用するには、BDA コンポーネントの機能を徹底的にテストして、BDA ネットワーク プロバイダー フィルターを使用して開始し、BDA コンポーネントのフィルターのインスタンスが含まれていますでレンダリングされ、少なくとも、デマルチプレクサーのフィルター (フィルター グラフを作成する必要があります。パケットの識別子 (PID) フィルター) をトランスポート情報フィルター (TIF)。 グラフ エディターを使用して最大の問題を使用して要求を送信する専用のアプリケーションがないこと、 **ITuner**ネットワーク プロバイダーのフィルターを実装するインターフェイス。 ただし、ネットワーク プロバイダーのフィルターが関連付けられている練習する限られたいくつか機能を提供するプロパティ ページ、 **ITuner**インターフェイス。

 

 




