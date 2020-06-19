---
title: AVStream のハードウェア コーデックのサポート
description: AVStream でのハードウェアコーデックのサポート
ms.assetid: 19ffd906-e198-4ede-b132-45e53431603c
keywords:
- AVStream WDK、ハードウェアコーデックサポート
- ハードウェアコーデックサポート WDK AVStream
- AVStream ハードウェアコーデックサポート WDK
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 04c941ec153dc6ba61afe477c26c25d2b99e0b4a
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992476"
---
# <a name="hardware-codec-support-in-avstream"></a>AVStream でのハードウェアコーデックのサポート

AVStream ベースのメディアデバイスは、ユーザーモードアプリケーションにメディアファンデーション変換 (MFT) フィルターとして表示できます。

この機能を使用すると、ハードウェアベンダーは、ハードウェアベースのデコーダー、エンコーダー、およびビデオプロセッサをユーザーモードのメディアファンデーション変換 (MFTs) として表示できます。

ハードウェアベースのエンコードとデコードによって、ユーザーエクスペリエンスが大幅に向上します。

AVStream でハードウェアコーデックのサポートを有効にするために、ベンダは、デコード、エンコーディング、およびビデオ処理を個別の AVStream フィルターとして公開する AVStream ベースのミニドライバーを提供します。 次に、オペレーティングシステムによって、各 AVStream フィルターに対応するユーザーモードの MFT が作成されます。 ユーザーモードのアプリケーションは、[メディアファンデーション SDK](https://docs.microsoft.com/windows/win32/medfound/microsoft-media-foundation-sdk)で定義されている IMFTransform インターフェイス関数を使用して、mfts にトランスコード要求を送信できます。

このセクションでは、AVStream ドライバーがこの機能を使用するために必要な変更について説明します。

このセクションでは、以下のトピックについて説明します。

[AVStream のハードウェア コーデック サポートの概要](getting-started-with-hardware-codec-support-in-avstream.md)

[AVStream コーデックのデータ型ネゴシエーションの処理](handling-data-type-negotiation-in-avstream-codecs.md)

[AVStream コーデックのハードウェア メディアの使用](using-hardware-mediums-in-avstream-codecs.md)

[AVStream コーデックのアロケーターのフレーム処理の指定](specifying-allocator-framing-in-avstream-codecs.md)

[AVStream コーデックの拡張サンプル情報の記述](describing-extended-sample-information-in-avstream-codecs.md)

[AVStream コーデックの動的形式変更のサポート](supporting-dynamic-format-changes-in-avstream-codecs.md)

[AVStream コーデックのストリームの終了処理](handling-end-of-stream-in-avstream-codecs.md)

[AVStream コーデックの状態のリセット](resetting-state-in-avstream-codecs.md)

[AVStream コーデックのストライド処理](handling-stride-in-avstream-codecs.md)

[AVStream ベースのハードウェア コーデック ドライバーのインストール](installing-an-avstream-based-hardware-codec-driver.md)
