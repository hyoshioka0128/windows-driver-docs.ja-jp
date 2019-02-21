---
title: いる CoNDIS ミニポート ドライバーの状態インジケーター
description: いる CoNDIS ミニポート ドライバーの状態インジケーター
ms.assetid: 1f1174ba-8b0a-4d43-96c9-2d92f50a22c4
keywords:
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS ミニポート ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a815ef4b31ca0d59fc23c9383a00dc4fe5310a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553949"
---
# <a name="condis-miniport-driver-status-indications"></a>いる CoNDIS ミニポート ドライバーの状態インジケーター





ミニポート ドライバーの呼び出し、 [ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)ミニポート アダプターの状態の変更を報告する関数。 ミニポート ドライバー パス**NdisMCoIndicateStatusEx**へのポインター、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)を含む構造体、状態情報。

状態の表示には、状態と状態の変更の理由の種類を識別する情報が含まれます。

ミニポート ドライバーを設定する必要があります、 **SourceHandle**の NDIS メンバー\_状態\_に渡される NDIS ハンドルを示す値構造体、 *MiniportAdapterHandle*パラメーター、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 状態の表示が OID 要求に関連付けられている場合は、ミニポート ドライバーを設定できます、 **DestinationHandle**と**RequestId** NDIS のメンバー\_状態\_INDICATION ようにその NDIS は、特定のプロトコル バインドを状態を示す値を提供できます。 OID 要求の詳細については、次を参照してください。[いる CoNDIS ミニポート ドライバーの OID 要求](condis-miniport-driver-oid-requests.md)します。

 

 





