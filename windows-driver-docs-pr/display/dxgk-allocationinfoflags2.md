---
title: '\_DXGK\_ALLOCATIONINFOFLAGS2 構造体'
description: DXGK\_ALLOCATIONINFOFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 67c27f53-29f0-4639-a360-0dbf7f3b3849
keywords:
- _DXGK_ALLOCATIONINFOFLAGS2 構造体のディスプレイ デバイス
- DXGK_ALLOCATIONINFOFLAGS2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONINFOFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e868b54ec7dec952c338f98cdcc02b35e69c258f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389988"
---
# <a name="dxgkallocationinfoflags2-structure"></a>\_DXGK\_ALLOCATIONINFOFLAGS2 構造体


DXGK\_ALLOCATIONINFOFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONINFOFLAGS2 {
  union {
    struct {
      UINT CpuVisible;
      UINT ReadOnly;
      UINT PermanentSysMem;
      UINT Cached;
      UINT ExistingSysMem;
      UINT ExistingKernelSysMem;
      UINT Swizzled;
      UINT Overlay;
      UINT Capture;
      UINT SynchronousPaging;
      UINT LinkMirrored;
      UINT LinkInstanced;
      UINT HistoryBuffer  :1;
      UINT Reserved  :2;
      UINT DXGK_ALLOC_RESERVED16  :1;
      UINT DXGK_ALLOC_RESERVED15  :1;
      UINT DXGK_ALLOC_RESERVED14  :1;
      UINT DXGK_ALLOC_RESERVED13  :1;
      UINT DXGK_ALLOC_RESERVED12  :1;
      UINT DXGK_ALLOC_RESERVED11  :1;
      UINT DXGK_ALLOC_RESERVED9  :1;
      UINT DXGK_ALLOC_RESERVED8  :1;
      UINT DXGK_ALLOC_RESERVED7  :1;
      UINT DXGK_ALLOC_RESERVED6  :1;
      UINT DXGK_ALLOC_RESERVED5  :1;
      UINT DXGK_ALLOC_RESERVED4  :1;
      UINT DXGK_ALLOC_RESERVED3  :1;
      UINT DXGK_ALLOC_RESERVED2  :1;
      UINT DXGK_ALLOC_RESERVED1  :1;
      UINT DXGK_ALLOC_RESERVED0  :1;
    };
    UINT Value;
  };
} DXGK_ALLOCATIONINFOFLAGS2;
```

<a name="members"></a>メンバー
-------

**CpuVisible**

**ReadOnly**

**PermanentSysMem**

**キャッシュ**

**ExistingSysMem**

**ExistingKernelSysMem**

**スィズル**

**オーバーレイ**

**キャプチャ**

**SynchronousPaging**

**LinkMirrored**

**LinkInstanced**

**HistoryBuffer**

**Reserved**

**DXGK\_アロケーション\_RESERVED16**

**DXGK\_ALLOC\_RESERVED15**

**DXGK\_ALLOC\_RESERVED14**

**DXGK\_アロケーション\_RESERVED13**

**DXGK\_アロケーション\_予約済み 12**

**DXGK\_ALLOC\_RESERVED11**

**DXGK\_ALLOC\_RESERVED9**

**DXGK\_ALLOC\_RESERVED8**

**DXGK\_アロケーション\_RESERVED7**

**DXGK\_ALLOC\_RESERVED6**

**DXGK\_ALLOC\_RESERVED5**

**DXGK\_ALLOC\_RESERVED4**

**DXGK\_アロケーション\_RESERVED3**

**DXGK\_ALLOC\_RESERVED2**

**DXGK\_アロケーション\_RESERVED1**

**DXGK\_ALLOC\_RESERVED0**

**値**

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
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。 Windows 8.1 で更新されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h (include D3dkmddi.h)</td>
</tr>
</tbody>
</table>

 

 





