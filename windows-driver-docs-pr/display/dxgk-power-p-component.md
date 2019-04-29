---
title: DXGK\_POWER\_P\_コンポーネントの構造
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 31D76B3B-E939-404B-9EE4-FFCDFCD304C8
keywords:
- DXGK_POWER_P_COMPONENT 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_POWER_P_COMPONENT
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d296e8b9263827c28acc00dbf7992029464a0991
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392035"
---
# <a name="dxgkpowerpcomponent-structure"></a>DXGK\_POWER\_P\_コンポーネントの構造


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_POWER_P_COMPONENT {
  ULONG                        StateCount;
  DXGK_POWER_P_STATE           States[DXGK_MAX_P_STATES];
  DXGK_POWER_COMPONENT_P_FLAGS Flags;
} DXGK_POWER_P_COMPONENT;
```

<a name="members"></a>メンバー
-------

**StateCount**

**状態**

**フラグ**

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h (include D3dkmddi.h)</td>
</tr>
</tbody>
</table>

 

 





