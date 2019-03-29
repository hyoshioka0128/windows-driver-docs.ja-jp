---
title: OID_GEN_VENDOR_DRIVER_VERSION
description: クエリとして OID_GEN_VENDOR_DRIVER_VERSION OID には、ミニポート ドライバーのベンダーが割り当てたバージョン番号を指定します。
ms.assetid: 37CB6A21-9AF2-49BF-AFBA-868C0C6C5383
keywords:
- OID_GEN_VENDOR_DRIVER_VERSION
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e69adabe84a2320f4e9e28209b7d7e64817d0cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574427"
---
# <a name="oidgenvendordriverversion"></a>OID_GEN_VENDOR_DRIVER_VERSION

クエリとして OID_GEN_VENDOR_DRIVER_VERSION OID には、ミニポート ドライバーのベンダーが割り当てたバージョン番号を指定します。

要求のセットがサポートされていません。

## <a name="remarks"></a>コメント

戻り値の下位半分; マイナー バージョンを指定します上位の半分には、メジャー バージョンを指定します。

この OID は、NDIS 6.0 およびそれ以降のミニポート ドライバーでは必須です。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

