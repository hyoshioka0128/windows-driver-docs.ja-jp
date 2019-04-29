---
title: '\_DXGKARG\_MOVEPAGEDIRECTORY 構造体'
description: DXGKARG\_MOVEPAGEDIRECTORY 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 81db1be9-4673-4353-b85f-8c6b87da1fc2
keywords:
- _DXGKARG_MOVEPAGEDIRECTORY 構造体のディスプレイ デバイス
- DXGKARG_MOVEPAGEDIRECTORY 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_MOVEPAGEDIRECTORY
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e74f8a20fe41acee0fa28176ca88d334d3e180af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384495"
---
# <a name="dxgkargmovepagedirectory-structure"></a>\_DXGKARG\_MOVEPAGEDIRECTORY 構造体


DXGKARG\_MOVEPAGEDIRECTORY 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_MOVEPAGEDIRECTORY {
  PVOID            pPageDirectory;
  PHYSICAL_ADDRESS PhysicalAddress;
  UINT             Segment;
  UINT             SizeInPages;
} DXGKARG_MOVEPAGEDIRECTORY;
```

<a name="members"></a>メンバー
-------

**pPageDirectory**システム用に予約されています。

**PhysicalAddress**システム用に予約されています。

**セグメント**システム用に予約されています。

**SizeInPages**システム用に予約されています。

<a name="requirements"></a>必要条件
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

 

 





