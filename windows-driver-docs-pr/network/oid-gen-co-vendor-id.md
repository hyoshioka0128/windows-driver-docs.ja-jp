---
title: OID_GEN_CO_VENDOR_ID
description: このトピックでは、OID_GEN_CO_VENDOR_ID オブジェクト識別子 (OID) について説明します。
ms.assetid: ec8d47e4-0b2f-4ca8-9227-330030a2ede5
keywords:
- OID_GEN_CO_VENDOR_ID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4c51320642946d336a806d553cffa33f5fc5d4
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917020"
---
# <a name="oid_gen_co_vendor_id"></a>OID_GEN_CO_VENDOR_ID

IEEE に登録された3バイトのベンダーコード。その後に、ベンダーが特定の NIC を識別するために割り当てる1バイトが続きます。

IEEE コードはベンダーを一意に識別し、NIC ハードウェアアドレスの先頭に表示される3バイトと同じです。

IEEE に登録されたコードのないベンダーは、値0xFFFFFF を使用する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

