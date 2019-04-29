---
title: DXGK\_SEGMENTDESCRIPTOR2 構造体
description: DXGK\_SEGMENTDESCRIPTOR2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 94eb1c9a-919c-4819-848b-29106e216980
keywords:
- DXGK_SEGMENTDESCRIPTOR2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_SEGMENTDESCRIPTOR2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2c0ea78370d3b2975c3ee8e934067c79a27d8098
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392029"
---
# <a name="dxgksegmentdescriptor2-structure"></a>DXGK\_SEGMENTDESCRIPTOR2 構造体


DXGK\_SEGMENTDESCRIPTOR2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_SEGMENTDESCRIPTOR2 {
  DXGK_SEGMENTFLAGS2 Flags;
  SIZE_T             Size;
  PMDL               pMdl;
  PHYSICAL_ADDRESS   BaseAddress;
  PHYSICAL_ADDRESS   CpuTranslatedAddress;
} DXGK_SEGMENTDESCRIPTOR2;
```

<a name="members"></a>メンバー
-------

**フラグ**システム用に予約されています。

**サイズ**システム用に予約されています。

**pMdl**システム用に予約されています。

**BaseAddress**システム用に予約されています。

**CpuTranslatedAddress**システム用に予約されています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h (include D3dkmddi.h)</td>
</tr>
</tbody>
</table>

 

 





