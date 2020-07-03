---
title: OID_GEN_CO_SUPPORTED_LIST
description: このトピックでは、OID_GEN_CO_SUPPORTED_LIST オブジェクト識別子 (OID) について説明します。
ms.assetid: 51c2b7f5-8429-4609-b048-542a3509f645
keywords:
- OID_GEN_CO_SUPPORTED_LIST
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c711692d10de29fe375c1769b6034ec1bd45f615
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917028"
---
# <a name="oid_gen_co_supported_list"></a>OID_GEN_CO_SUPPORTED_LIST

OID_GEN_CO_SUPPORTED_LIST OID は、基になるドライバーまたはその NIC がサポートするオブジェクトの Oid の配列を指定します。 オブジェクトには、汎用、メディア固有、および実装固有のオブジェクトが含まれます。

基になるドライバーは、返される OID リストを数値の昇順に並べ替える必要があります。 NDIS は、返された一覧のサブセットを、このクエリを実行するプロトコルに転送します。 つまり、プロトコルによって統計クエリが行われることはないため、NDIS はサポートされているすべての統計 Oid を一覧から除外します。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

