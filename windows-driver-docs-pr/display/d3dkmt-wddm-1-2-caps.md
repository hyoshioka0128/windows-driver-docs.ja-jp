---
title: D3DKMT\_WDDM\_1\_2\_CAPS 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 0cd26fad-4772-4631-81fc-da2ddb7dc9a1
keywords:
- D3DKMT_WDDM_1_2_CAPS 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_WDDM_1_2_CAPS
api_location:
- D3dkmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6694172357f1e9ca3a0423819e9312347bf54af8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382941"
---
# <a name="d3dkmtwddm12caps-structure"></a>D3DKMT\_WDDM\_1\_2\_CAPS 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_WDDM_1_2_CAPS {
  D3DKMDT_PREEMPTION_CAPS PreemptionCaps;
  union {
    struct {
      UINT SupportNonVGA  :1;
      UINT SupportSmoothRotation  :1;
      UINT SupportPerEngineTDR  :1;
      UINT SupportKernelModeCommandBuffer  :1;
      UINT SupportCCD  :1;
      UINT SupportSoftwareDeviceBitmaps  :1;
      UINT SupportGammaRamp  :1;
      UINT SupportHWCursor  :1;
      UINT SupportHWVSync  :1;
      UINT SupportSurpriseRemovalInHibernation  :1;
      UINT Reserved  :22;
    };
    UINT   Value;
  };
} D3DKMT_WDDM_1_2_CAPS;
```

<a name="members"></a>メンバー
-------

**PreemptionCaps**

**SupportNonVGA**

**SupportSmoothRotation**

**SupportPerEngineTDR**

**SupportKernelModeCommandBuffer**

**SupportCCD**

**SupportSoftwareDeviceBitmaps**

**SupportGammaRamp**

**SupportHWCursor**

**SupportHWVSync**

**SupportSurpriseRemovalInHibernation**

**Reserved**

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
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmdt.h (D3dkmdt.h を含む)</td>
</tr>
</tbody>
</table>

 

 





