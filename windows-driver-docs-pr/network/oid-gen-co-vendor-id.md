---
title: OID_GEN_CO_VENDOR_ID
description: このトピックでは、OID_GEN_CO_VENDOR_ID オブジェクト識別子 (OID) について説明します。
ms.assetid: ec8d47e4-0b2f-4ca8-9227-330030a2ede5
keywords:
- OID_GEN_CO_VENDOR_ID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47e03f2ae75759b27d09d33edcc463fa6de7097a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557221"
---
# <a name="oidgencovendorid"></a>OID_GEN_CO_VENDOR_ID

仕入先が特定の NIC を識別するために代入する 1 バイトの後に、3 バイト IEEE に登録されたベンダー コード

IEEE コードは一意にベンダーを識別し、NIC のハードウェア アドレスの先頭に表示される 3 つのバイト数と同じです。

ベンダーは、IEEE 登録コードなしでは、値 0 xffffff を使用してください。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

