---
title: ネットワーク インターフェイスの登録解除
description: ネットワーク インターフェイスの登録解除
ms.assetid: 8d290a6a-008d-434b-bcbf-c4efade3d017
keywords:
- NDIS ネットワーク インターフェイス、WDK の登録を解除
- ネットワーク インターフェイス、WDK の登録を解除
- ネットワーク インターフェイスを登録解除
- ネットワーク インターフェイスを削除します。
- ネットワーク インターフェイスを登録解除
- NdisIfDeregisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70384152e71bfb216320abf95643941aff1f6fd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579820"
---
# <a name="deregistering-a-network-interface"></a>ネットワーク インターフェイスの登録解除





NDIS インターフェイスのプロバイダーを呼び出し、 [ **NdisIfDeregisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562700)をコンピューターの既知のインターフェイスの一覧から指定されたインターフェイスをたとえば、削除する必要があるかを示す関数インターフェイスがアンインストールされました。 インターフェイスを登録解除の他の理由は、アプリケーション固有です。 適切なリソースの管理を昇格するには、プロバイダーのインターフェイスはもはやインターフェイスを登録解除は常にします。

**NdisIfDeregisterInterface**指定されたインターフェイスに関連付けられているインターフェイス インデックスを解放します。 NDIS は、将来的に登録されているインターフェイスのインデックスを再割り当てできます。 ただし、 [ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)インデックスに関連付けられた対応する NET\_LUID 値は再利用できません--必要に応じて、インターフェイスのプロバイダーは、NET をリリースできます\_LUID のインデックスを呼び出して、 [ **NdisIfFreeNetLuidIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562706)関数。

**注**  がアンインストールされ、デタッチされたときに、モジュールをフィルター処理するときに、NDIS プロキシ プロバイダー登録ミニポート アダプター用のインターフェイスを解除します。

 

 

 





