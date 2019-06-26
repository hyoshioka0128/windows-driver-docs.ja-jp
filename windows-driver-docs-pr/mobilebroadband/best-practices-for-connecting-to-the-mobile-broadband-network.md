---
title: モバイル ブロードバンド ネットワークに接続するためのベスト プラクティス
description: モバイル ブロードバンド ネットワークに接続するためのベスト プラクティス
ms.assetid: 6106d026-1c5f-4990-8ef2-467c1a77a38e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfe730a408b7dc61089d1aff6c0305330189d882
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365000"
---
# <a name="best-practices-for-connecting-to-the-mobile-broadband-network"></a>モバイル ブロードバンド ネットワークに接続するためのベスト プラクティス


モバイル ブロード バンド ネットワークにアクティブな接続は、バッテリの寿命とアカウントのデータ クォータに不要なドレインを指定できます。 慎重に判断を使用して、接続が必要かどうかを判断することをお勧めします。

モバイル ブロード バンド ネットワークへの接続に関する次のベスト プラクティスを使用します。

-   エージェントのプロビジョニングを使用しないでください&lt;*アクティベーション*&gt;ディレクティブ。 これらのディレクティブは特定の状況に対してのみアクティブ化の後に対象としています。

-   一時的な接続を確立するのにには、モバイル ブロード バンド API を使用します。 この API は、操作の結果の接続および切断する簡単な方法を提供します。

-   接続の有効期間を最小限に抑えます。

-   利用できる場合は、インターネットに接続されたインターフェイスを介して接続を使用します。 使用して可用性を確認することができます、 [ **NetworkInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation) API。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム API を使用するためのベスト プラクティス](best-practices-for-using-mobile-broadband-windows-runtime-api.md)

 

 






