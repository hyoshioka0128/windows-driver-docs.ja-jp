---
title: KMDF ドライバーのデバッグに関するビデオ
description: このトピックには、カーネルモードドライバーフレームワーク (KMDF) ドライバーをデバッグする方法を示す、Kumar Rajeev の3部構成のビデオシリーズへのリンクが含まれています。
ms.assetid: 62D0F1DA-318F-4989-94C5-968C67F420C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b76d614462b0105619dcdd2f5e6ec4bd182915
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210500"
---
# <a name="videos-debugging-kmdf-drivers"></a>ビデオ: KMDF ドライバーのデバッグ


このトピックには、カーネルモードドライバーフレームワーク (KMDF) ドライバーをデバッグする方法を示す、Kumar Rajeev の3部構成のビデオシリーズへのリンクが含まれています。

ビデオを視聴した後、KMDF デバッガーの拡張機能について理解し、基本的なデバッグシナリオでそれらを使用する方法を理解することができます。

## <a name="prerequisites"></a>前提条件


この一連のデモは、高度な技術レベルで提供されています。 このコンテンツを最大限に活用するには、Windows カーネルデバッガー (windbg) に関する実用的な知識が必要です。また、KMDF を使用したコードの作成と使用について理解している必要があります。 各セッションは前のセッションを基にしているため、これらのデモは記載されている順序で表示することをお勧めします。

## <a name="video-series-debugging-kernel-mode-driver-framework-drivers"></a>ビデオシリーズ: カーネルモードドライバーフレームワークドライバーのデバッグ


-   [セッション 1: KMDF ログのダンプ (10 分)](https://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-1.wmv) \[メディアファイル\]

    KMDF ログは、問題の根本原因をすばやく特定するのに役立つ重要な機能です。 このセッションでは、カーネルデバッガーで KMDF ログをダンプする方法を示します。 また、ログのサイズと詳細度を変更する方法についても説明し、ログのスキャンに関するヒントを示します。

-   [セッション 2: KMDF ドライバーとそのオブジェクト (15 分) \[のメディアファイルに関する情報を取得する](https://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-2.wmv)\]

    KMDF には、ドライバーに関するさまざまな種類の情報を調査するのに役立つデバッガーコマンドがいくつか用意されています。 このセッションでは、KMDF ドライバーによって作成されたすべてのフレームワークオブジェクト (親子階層、検証ツールの状態、デバイス階層など) をダンプする方法を示します。 これらのコマンドは、通常、より詳細な調査の出発点となります。

-   [セッション 3: デバイスとキューのダンプ (15 分)](https://download.microsoft.com/download/B/5/E/B5ECC1FC-7408-461C-B226-CF3AE3E3873F/Debugging-KMDF-Drivers-Part-3.wmv) \[メディアファイル\]

    このセッションでは、KMDF デバイスオブジェクトに関する詳細情報を取得する方法について説明します。これには、プラグアンドプレイ (PnP) と電源の状態、電源ポリシーの所有権、電源設定、PnP と電源コールバック、デバイスプロパティなどが含まれます。 また、開いているハンドルに関する情報を取得し、デバイス用に構成されているすべての i/o キューを探索して、個々の要求をダンプする方法についても説明します。

 

 





