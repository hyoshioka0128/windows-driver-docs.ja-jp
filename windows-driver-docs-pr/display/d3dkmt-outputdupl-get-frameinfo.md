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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346257"
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

<a name="members"></a>メンバー
-------

**hAdapter**

**VidPnSourceId**

**FrameInfo**

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

 

 





