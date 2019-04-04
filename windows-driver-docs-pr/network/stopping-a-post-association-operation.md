---
title: 後の関連付け操作を停止します。
description: 後の関連付け操作を停止します。
ms.assetid: 28400cad-1e77-4bcd-9b9a-103df5f06d10
keywords:
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 後の関連付け操作を停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b70ce65f72852e7554c66271163aea4911ffb3b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535876"
---
# <a name="stopping-a-post-association-operation"></a>後の関連付け操作を停止します。




 

オペレーティング システムが呼び出すことによって、後の関連付け操作を終了、 [ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521)次のいずれかが発生するたびに、IHV ハンドラー関数。

-   ワイヤレス LAN (WLAN) アダプターは、AP との関連付け解除操作を完了します。 このような状況で、アダプターを管理するには、ネイティブの 802.11 ステーションは、メディア固有[NDIS\_状態\_DOT11\_戻せません](https://msdn.microsoft.com/library/windows/hardware/ff567334)を示す値。 関連付け解除操作の詳細については、[関連付け解除操作](disassociation-operations.md)を参照してください。

-   WLAN アダプターが無効にしたり、削除します。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521)関数を呼び出す前に、 [ *Dot11ExtIhvDeinitAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff547452)関数。

オペレーティング システムの呼び出し、 [ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521) AP との関連付けの作成、データ ポートがダウンした IHV 拡張 DLL に通知します。 オペレーティング システムが DLL を呼び出すことによって、後の関連付け操作が完了したかどうかに関係なく、この関数を呼び出す[ **Dot11ExtPostAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547530)します。

ときに[ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521)が呼び出されると、IHV 拡張する必要がありますリリースのすべてのデータ ポートに割り当てられたリソース。 後の関連付け操作がへの呼び出しで完了していないかどうかは[ **Dot11ExtPostAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547530)、IHV 拡張機能の DLL は、内部的には、操作を取り消す必要がありますを呼び出してはならない**Dot11ExtPostAssociateCompletion**します。

 

 





