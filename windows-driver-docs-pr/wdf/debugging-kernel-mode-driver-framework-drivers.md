---
title: KMDF ドライバーのデバッグのビデオ
description: このトピックには、カーネル モード ドライバー フレームワーク (KMDF) ドライバーをデバッグする方法を示す Kumar Rajeev で 3 部構成のビデオ シリーズへのリンクが含まれています。
ms.assetid: 62D0F1DA-318F-4989-94C5-968C67F420C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34255e1be2c2fad5f8e8f6241796212514bcb16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362451"
---
# <a name="videos-debugging-kmdf-drivers"></a>ビデオ: KMDF ドライバーのデバッグ


このトピックには、カーネル モード ドライバー フレームワーク (KMDF) ドライバーをデバッグする方法を示す Kumar Rajeev で 3 部構成のビデオ シリーズへのリンクが含まれています。

後は、ビデオ KMDF デバッガー拡張機能を熟知し、基本的なデバッグ シナリオで使用する方法を理解します。

## <a name="prerequisites"></a>前提条件


この一連のデモについては、高度な技術レベルで付与します。 このコンテンツを最大限には、Windows カーネル デバッガー (windbg.exe) の作業に関する知識が必要し、を作成して、KMDF でコードの使用について理解する必要があります。 各セッションは、1 つ前のビルド、ために、表示されている順序でこれらのデモを表示することをお勧めします。

## <a name="video-series-debugging-kernel-mode-driver-framework-drivers"></a>ビデオ シリーズ:カーネル モード ドライバー フレームワーク ドライバーのデバッグ


-   [セッション 1:KMDF ログ (10 分) のダンプ](http://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-1.wmv)\[メディア ファイル\]

    KMDF ログは、問題の根本原因をすばやく識別するのに役立つ重要な機能です。 このセッションでは、カーネル デバッガーで KMDF ログをダンプする方法を示します。 サイズと、ログの詳細度を変更する方法について説明し、ログのスキャンに関するヒントを提供します。

-   [セッション 2:KMDF ドライバーおよびそのオブジェクト (15 分) に関する情報を取得する](http://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-2.wmv)\[メディア ファイル\]

    KMDF を提供する際に役立ついくつかのデバッガー コマンドは、さまざまな種類のドライバーに関する情報を探索します。 このセッションでは、親子階層、検証の状態、およびデバイスの階層を含む、KMDF ドライバーによって作成されたすべての framework オブジェクトをダンプする方法を示します。 これらのコマンドは、通常より詳細な調査の開始点です。

-   [セッション 3:デバイスとキュー (15 分) のダンプ](http://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-3.wmv)\[メディア ファイル\]

    このセッションでは、プラグ アンド プレイ (PnP) と電源の状態、電源ポリシーの所有権、電源構成、PnP と電力のコールバック、およびデバイスのプロパティを含め、KMDF デバイス オブジェクトに関する詳細情報を取得する方法を示します。 これは、方法も示します開いているハンドルに関する情報を取得する、デバイス用に構成されたすべての I/O キューを参照および個々 の要求をダンプします。

 

 





