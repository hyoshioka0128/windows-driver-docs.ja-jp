---
title: D3DKMT\_OUTPUTDUPL\_ポインター\_位置構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: c05205bf-3f7c-487d-8cce-d708d50eb4d9
keywords:
- D3DKMT_OUTPUTDUPL_POINTER_POSITION 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_POINTER_POSITION
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 11f061784980ad578f8b9f68ea5ab5420669122c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379728"
---
# <a name="d3dkmtoutputduplpointerposition-structure"></a>D3DKMT\_OUTPUTDUPL\_ポインター\_位置構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_POINTER_POSITION {
  POINT Position;
  BOOL  Visible;
} D3DKMT_OUTPUTDUPL_POINTER_POSITION;
```

<a name="members"></a>メンバー
-------

**[Position]**

**表示されます。**

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmthk.h (D3dkmthk.h を含む)</td>
</tr>
</tbody>
</table>

 

 





