---
title: D3DKMT\_WDDM\_2\_0\_CAPS 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 90D2398F-C474-4D58-9EA2-5823E366E1C7
keywords:
- D3DKMT_WDDM_2_0_CAPS 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_WDDM_2_0_CAPS
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2285475e6da8a4a66c7e0ed5b44977a42db4bc62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382937"
---
# <a name="d3dkmtwddm20caps-structure"></a>D3DKMT\_WDDM\_2\_0\_CAPS 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_WDDM_2_0_CAPS {
  union {
    struct {
      UINT Support64BitAtomics  :1;
      UINT GpuMmuSupported  :1;
      UINT IoMmuSupported  :1;
      UINT Reserved  :29;
    };
    UINT   Value;
  };
} D3DKMT_WDDM_2_0_CAPS;
```

<a name="members"></a>メンバー
-------

**Support64BitAtomics**

**GpuMmuSupported**

**IoMmuSupported**

**Reserved**

**値**

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmdt.h (include D3dkmddi.h)</td>
</tr>
</tbody>
</table>

 

 





