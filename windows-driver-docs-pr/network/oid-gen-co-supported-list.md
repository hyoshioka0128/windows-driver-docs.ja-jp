---
title: OID_GEN_CO_SUPPORTED_LIST
description: このトピックでは、OID_GEN_CO_SUPPORTED_LIST オブジェクト識別子 (OID) について説明します。
ms.assetid: 51c2b7f5-8429-4609-b048-542a3509f645
keywords:
- OID_GEN_CO_SUPPORTED_LIST
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: f053e840ecc7994dbe7c8a0e94c9b04213bbacea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355727"
---
# <a name="oidgencosupportedlist"></a>OID_GEN_CO_SUPPORTED_LIST

OID_GEN_CO_SUPPORTED_LIST OID には、基になるドライバーまたはその NIC をサポートするオブジェクトの Oid の配列を指定します。 オブジェクトには、[全般]、メディア固有および実装に固有のオブジェクトが含まれます。

数値の昇順で返します OID 一覧の順序は、基になるドライバーが必要があります。 NDIS は、このクエリを構成するプロトコルに返されるリストのサブセットを転送します。 つまり、プロトコルで統計情報のクエリをその後ことはありませんので、NDIS は、リストからサポートされている統計 Oid をフィルター処理します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

