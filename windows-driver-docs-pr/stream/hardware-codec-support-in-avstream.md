---
title: AVStream でハードウェアのコーデック サポート
description: AVStream でハードウェアのコーデック サポート
ms.assetid: 19ffd906-e198-4ede-b132-45e53431603c
keywords:
- AVStream WDK、ハードウェアのコーデック サポート
- ハードウェアのコーデック サポート WDK AVStream
- AVStream ハードウェア コーデック サポート WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7908decf3f5e5355277d3e27eac4fd0f1011cf4e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553842"
---
# <a name="hardware-codec-support-in-avstream"></a>AVStream でハードウェアのコーデック サポート


Windows 7 および Windows の以降のバージョンでは、ユーザー モード アプリケーションに Media Foundation の変換 (MFT) フィルターとして AVStream ベースのメディア デバイスを表示できます。

この機能は、ユーザー モード Media Foundation 変換 (仕様) として、ハードウェア ベースのデコーダー、エンコーダー、およびビデオのプロセッサを提示する、ハードウェア ベンダーを使用できます。

ハードウェア ベースのエンコードとデコードが大幅には、ユーザー エクスペリエンスを向上します。

AVStream でハードウェアのコーデック サポートを有効にする、仕入先には、デコード、エンコード、およびビデオの処理、それぞれ別個の AVStream フィルターとして公開する AVStream ベース ミニドライバーが用意されています。 オペレーティング システムは、各 AVStream フィルターに対応するユーザー モード MFT を作成します。 ユーザー モード アプリケーションできますトランスコーディングに要求を送信、仕様で定義されている IMFTransform インターフェイス関数を使用して、 [Media Foundation SDK](https://go.microsoft.com/fwlink/p/?linkid=144771)します。

このセクションでは、この機能を使用する AVStream ドライバーに必要な変更について説明します。

このセクションには、次のトピックが含まれています。

[AVStream でハードウェアのコーデック サポートの概要](getting-started-with-hardware-codec-support-in-avstream.md)

[AVStream コーデックで処理データの種類のネゴシエーション](handling-data-type-negotiation-in-avstream-codecs.md)

[AVStream コーデックでハードウェアのメディアの使用](using-hardware-mediums-in-avstream-codecs.md)

[アロケーター AVStream コーデックでフレームを指定します。](specifying-allocator-framing-in-avstream-codecs.md)

[AVStream コーデックの拡張のサンプル情報を記述します。](describing-extended-sample-information-in-avstream-codecs.md)

[AVStream コーデックでの動的形式の変更のサポート](supporting-dynamic-format-changes-in-avstream-codecs.md)

[AVStream コーデックで Stream の最後の処理](handling-end-of-stream-in-avstream-codecs.md)

[AVStream コーデックで状態をリセットします。](resetting-state-in-avstream-codecs.md)

[AVStream コーデックのストライドを処理します。](handling-stride-in-avstream-codecs.md)

[コーデック AVStream ベースのハードウェア ドライバーをインストールします。](installing-an-avstream-based-hardware-codec-driver.md)

 

 




