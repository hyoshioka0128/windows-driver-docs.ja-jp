---
title: OID_GEN_VENDOR_DRIVER_VERSION
description: クエリとして、OID_GEN_VENDOR_DRIVER_VERSION OID は、ミニポートドライバーのベンダーによって割り当てられたバージョン番号を指定します。
ms.assetid: 37CB6A21-9AF2-49BF-AFBA-868C0C6C5383
keywords:
- OID_GEN_VENDOR_DRIVER_VERSION
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: f25991dd8620d6372252e4526f419606910c4c20
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917008"
---
# <a name="oid_gen_vendor_driver_version"></a>OID_GEN_VENDOR_DRIVER_VERSION

クエリとして、OID_GEN_VENDOR_DRIVER_VERSION OID は、ミニポートドライバーのベンダーによって割り当てられたバージョン番号を指定します。

Set 要求はサポートされていません。

## <a name="remarks"></a>注釈

戻り値の下位半分にはマイナーバージョンが指定されています。上位半分では、メジャーバージョンを指定します。

この OID は、NDIS 6.0 以降のミニポートドライバーに必須です。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

