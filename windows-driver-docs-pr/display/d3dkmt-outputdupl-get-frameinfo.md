---
title: D3DKMT\_OUTPUTDUPL\_取得\_FRAMEINFO 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: e358f8b6-623b-4dd0-82d7-5b46f31b26c7
keywords:
- D3DKMT_OUTPUTDUPL_GET_FRAMEINFO 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_GET_FRAMEINFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: cfefbd60b6066a3ea61ce0348a058a12301d8d13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549699"
---
# <a name="d3dkmtoutputduplgetframeinfo-structure"></a>D3DKMT\_OUTPUTDUPL\_取得\_FRAMEINFO 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_GET_FRAMEINFO {
  D3DKMT_HANDLE                  hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  D3DKMT_OUTPUTDUPL_FRAMEINFO    FrameInfo;
} D3DKMT_OUTPUTDUPL_GET_FRAMEINFO;
```

<a name="members"></a>Members
-------

**hAdapter**

**VidPnSourceId**

**FrameInfo**

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

 

 





