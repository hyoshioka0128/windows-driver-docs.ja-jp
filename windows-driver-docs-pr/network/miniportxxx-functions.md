---
title: MiniportXxx 関数
description: MiniportXxx 関数
ms.assetid: b992c3ff-deb1-49e2-a99f-310cc4cb81c3
keywords:
- MiniportXxx 関数 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e8fa1b3cd58acb8bcb935e48b66d57d0c1acdda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552189"
---
# <a name="miniportxxx-functions"></a>MiniportXxx 関数





一般的なミニポート ドライバーでは、関数の数が少ないを使用して、ハードウェアと上位層で NDIS 経由で通信します。 すべての機能が必要です。 関数の省略可能なについての詳細については、必要な場合と理由を参照してください[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

NDIS ミニポート ドライバーおよび上位層のドライバーは、呼び出しを通して互いと通信する NDIS ライブラリ (Ndis.sys) を使用して**Ndis * Xxx*** 関数。

多くのミニポート ドライバー関数は、同期または非同期に動作します。 非同期関数が**Ndis*Xxx*完了**操作が終了したときに呼び出す必要がある関数。 プロトコル ドライバーを呼び出す場合など、 [ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)ミニポート ドライバー情報のクエリ、ミニポート ドライバーの*MiniportOidRequest*関数できますを保留しますNDIS を返すことによってリセット操作\_状態\_保留します。 最終的に、ミニポート ドライバーを呼び出す必要があります[ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)のクエリ要求の最終的な状態を示します。

 

 





