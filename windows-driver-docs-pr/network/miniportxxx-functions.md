---
title: MiniportXxx 関数
description: MiniportXxx 関数
ms.assetid: b992c3ff-deb1-49e2-a99f-310cc4cb81c3
keywords:
- MiniportXxx 関数 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1ece15239edda28c6f381e5b973f9226a3ddbb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382213"
---
# <a name="miniportxxx-functions"></a>MiniportXxx 関数





一般的なミニポート ドライバーでは、関数の数が少ないを使用して、ハードウェアと上位層で NDIS 経由で通信します。 すべての機能が必要です。 関数の省略可能なについての詳細については、必要な場合と理由を参照してください[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

NDIS ミニポート ドライバーおよび上位層のドライバーは、呼び出しを通して互いと通信する NDIS ライブラリ (Ndis.sys) を使用して**Ndis * Xxx*** 関数。

多くのミニポート ドライバー関数は、同期または非同期に動作します。 非同期関数が**Ndis*Xxx*完了**操作が終了したときに呼び出す必要がある関数。 プロトコル ドライバーを呼び出す場合など、 [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)ミニポート ドライバー情報のクエリ、ミニポート ドライバーの*MiniportOidRequest*関数できますを保留しますNDIS を返すことによってリセット操作\_状態\_保留します。 最終的に、ミニポート ドライバーを呼び出す必要があります[ **NdisMOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)のクエリ要求の最終的な状態を示します。

 

 





