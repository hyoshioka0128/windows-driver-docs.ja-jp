---
title: OID_GEN_VENDOR_DRIVER_VERSION
description: クエリとして OID_GEN_VENDOR_DRIVER_VERSION OID には、ミニポート ドライバーのベンダーが割り当てたバージョン番号を指定します。
ms.assetid: 37CB6A21-9AF2-49BF-AFBA-868C0C6C5383
keywords:
- OID_GEN_VENDOR_DRIVER_VERSION
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e69adabe84a2320f4e9e28209b7d7e64817d0cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387866"
---
# <a name="oidgenvendordriverversion"></a>OID_GEN_VENDOR_DRIVER_VERSION

クエリとして OID_GEN_VENDOR_DRIVER_VERSION OID には、ミニポート ドライバーのベンダーが割り当てたバージョン番号を指定します。

要求のセットがサポートされていません。

## <a name="remarks"></a>注釈

戻り値の下位半分; マイナー バージョンを指定します上位の半分には、メジャー バージョンを指定します。

この OID は、NDIS 6.0 およびそれ以降のミニポート ドライバーでは必須です。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

