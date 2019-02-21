---
title: クエリの NDIS QoS 機能
description: クエリの NDIS QoS 機能
ms.assetid: 00A2EFCD-CD90-446C-B588-EC66E3E730B2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79f4c4a77d0c8154c56cc57c74d8f9dcb5c8037a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536251"
---
# <a name="querying-ndis-qos-capabilities"></a>クエリの NDIS QoS 機能


プロトコルとフィルター ドライバーに関連は次のように、ネットワーク アダプターの NDIS サービスの品質 (QoS) 機能を照会できます。

-   上にあるドライバーは、オブジェクト識別子 (OID) のクエリ要求のを通じてネットワーク アダプターでサポートされているハードウェアの NDIS QoS 機能を照会できます[OID\_QOS\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/hh451828)します。

-   上にあるドライバーは現在の OID クエリ要求を使ってネットワーク アダプターで有効になっているハードウェアの NDIS QoS 機能を照会できます[OID\_QOS\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/hh451827)します。

NDIS は、ミニポート ドライバーのこれらの OID 要求を処理します。 登録すると、ミニポート ドライバー ハードウェアおよびネットワーク アダプターの NDIS QoS 機能が現在有効なネットワーク アダプターの初期化中に、NDIS は、この情報をキャッシュします。 NDIS は、上にある、ドライバーから OID の要求を処理する場合、このデータを返します。

ミニポート ドライバーが NDIS QoS 機能を登録する方法の詳細については、次を参照してください。 [NDIS QoS 機能の登録](registering-ndis-qos-capabilities.md)します。

 

 





