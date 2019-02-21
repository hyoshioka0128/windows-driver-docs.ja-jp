---
title: いる CoNDIS プロトコル ドライバーの処理状態のインジケーター
description: いる CoNDIS プロトコル ドライバーの処理状態のインジケーター
ms.assetid: 948df51b-0561-4b67-b87f-e1652bb18772
keywords:
- プロトコル ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS プロトコル ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab0a234cf2f2e1f851d39b5827153b9c46b22766
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532353"
---
# <a name="handling-status-indications-in-a-condis-protocol-driver"></a>いる CoNDIS プロトコル ドライバーの処理状態のインジケーター





プロトコル ドライバーを指定する必要があります、 [ **ProtocolCoStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570258) NDIS が、基になるドライバーの状態を報告したときに呼び出す関数です。

NDIS 呼び出しプロトコル ドライバーの*ProtocolCoStatusEx*関数の状態を示す値の関数を呼び出して、基になるドライバーから (たとえば、 [ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)). 詳細については、ミニポート ドライバーからの状態を示す、次を参照してください。[いる CoNDIS ミニポート ドライバーの状態インジケーター](condis-miniport-driver-status-indications.md)します。

状態の表示が OID 要求に関連付けられている場合は、基になるドライバーを設定できます、 **DestinationHandle**と**RequestId**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373) NDIS は、特定のプロトコル バインドに、状態を示す値を提供できるように、状態情報を含む構造体。 OID 要求の詳細については、次を参照してください。[いる CoNDIS プロトコル ドライバー OID 要求](condis-protocol-driver-oid-requests.md)します。

 

 





