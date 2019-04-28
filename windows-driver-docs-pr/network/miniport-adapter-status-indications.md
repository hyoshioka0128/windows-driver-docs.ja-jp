---
title: ミニポート アダプター状態表示
description: ミニポート アダプター状態表示
ms.assetid: feb5259f-ce9b-40eb-85d2-0064bce692fc
keywords:
- 状態インジケーターの WDK ネットワー キング、ミニポート アダプター
- ミニポート アダプタの WDK ネットワー キング、状態インジケーター
- アダプターの WDK ネットワー キング、状態インジケーター
- NdisMIndicateStatusEx
- NDIS_STATUS_INDICATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ddead5af15fc7a1527fc3cd1cb65acd58105d1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379807"
---
# <a name="miniport-adapter-status-indications"></a>ミニポート アダプター状態表示





ミニポート ドライバーの呼び出し、 [ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)ミニポート アダプターの状態の変更を報告する関数。 ミニポート ドライバー パス**NdisMIndicateStatusEx**へのポインター、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)を含む構造体、状態情報。

状態の表示には、状態と状態の変更の理由の種類を識別する情報が含まれます。

ミニポート ドライバーを設定する必要があります、 **SourceHandle**に渡される NDIS ハンドルへのメンバー、 *MiniportAdapterHandle*のパラメーター、 [ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 状態の表示が OID 要求に関連付けられている場合は、ミニポート ドライバーを設定できます、 **DestinationHandle**と**RequestId**その NDIS は、特定の状態の表示を提供できるように、メンバープロトコル バインディング。

 

 





