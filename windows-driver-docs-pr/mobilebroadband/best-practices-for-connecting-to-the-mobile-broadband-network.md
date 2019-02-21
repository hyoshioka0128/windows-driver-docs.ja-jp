---
title: モバイル ブロード バンド ネットワークに接続するためのベスト プラクティス
description: モバイル ブロード バンド ネットワークに接続するためのベスト プラクティス
ms.assetid: 6106d026-1c5f-4990-8ef2-467c1a77a38e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bed901b901260f9b9fb1927fe1ebac785b150a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528318"
---
# <a name="best-practices-for-connecting-to-the-mobile-broadband-network"></a>モバイル ブロード バンド ネットワークに接続するためのベスト プラクティス


モバイル ブロード バンド ネットワークにアクティブな接続は、バッテリの寿命とアカウントのデータ クォータに不要なドレインを指定できます。 慎重に判断を使用して、接続が必要かどうかを判断することをお勧めします。

モバイル ブロード バンド ネットワークへの接続に関する次のベスト プラクティスを使用します。

-   エージェントのプロビジョニングを使用しないでください&lt;*アクティベーション*&gt;ディレクティブ。 これらのディレクティブは特定の状況に対してのみアクティブ化の後に対象としています。

-   一時的な接続を確立するのにには、モバイル ブロード バンド API を使用します。 この API は、操作の結果の接続および切断する簡単な方法を提供します。

-   接続の有効期間を最小限に抑えます。

-   利用できる場合は、インターネットに接続されたインターフェイスを介して接続を使用します。 使用して可用性を確認することができます、 [ **NetworkInformation** ](https://msdn.microsoft.com/library/windows/apps/br207293) API。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム API を使用するためのベスト プラクティス](best-practices-for-using-mobile-broadband-windows-runtime-api.md)

 

 






