---
title: D3DKMT\_UNPINDIRECTFLIPRESOURCES 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: c875a30c-41e4-478c-b8b0-c1fb32672915
keywords:
- D3DKMT_UNPINDIRECTFLIPRESOURCES 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_UNPINDIRECTFLIPRESOURCES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e349daa5992e9e8934c50a55442d6a2714397138
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536337"
---
# <a name="d3dkmtunpindirectflipresources-structure"></a>D3DKMT\_UNPINDIRECTFLIPRESOURCES 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_UNPINDIRECTFLIPRESOURCES {
  D3DKMT_HANDLE hDevice;
  UINT          ResourceCount;
  D3DKMT_HANDLE *pResourceList;
} D3DKMT_UNPINDIRECTFLIPRESOURCES;
```

<a name="members"></a>Members
-------

**hDevice**

**ResourceCount**

**pResourceList**

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

 

 





