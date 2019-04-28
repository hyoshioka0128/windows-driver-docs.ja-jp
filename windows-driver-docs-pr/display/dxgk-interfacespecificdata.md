---
title: DXGK\_INTERFACESPECIFICDATA 構造体
description: DXGK\_INTERFACESPECIFICDATA 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: dc9ad39c-4439-4e01-9825-fc1df3c3adc0
keywords:
- DXGK_INTERFACESPECIFICDATA 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_INTERFACESPECIFICDATA
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc207b66151d857f8e0f810d440e2247f3f79147
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372969"
---
# <a name="dxgkinterfacespecificdata-structure"></a>DXGK\_INTERFACESPECIFICDATA 構造体


DXGK\_INTERFACESPECIFICDATA 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_INTERFACESPECIFICDATA {
  HANDLE                     hAdapter;
  DXGKCB_GETHANDLEDATA       pfnGetHandleDataCb;
  DXGKCB_GETHANDLEPARENT     pfnGetHandleParentCb;
  DXGKCB_ENUMHANDLECHILDREN  pfnEnumHandleChildrenCb;
  DXGKCB_NOTIFY_INTERRUPT    pfnNotifyInterruptCb;
  DXGKCB_NOTIFY_DPC          pfnNotifyDpcCb;
  DXGKCB_QUERYVIDPNINTERFACE pfnQueryVidPnInterfaceCb;
  DXGKCB_GETCAPTUREADDRESS   pfnGetCaptureAddressCb;
} DXGK_INTERFACESPECIFICDATA;
```

<a name="members"></a>メンバー
-------

**hAdapter**システム用に予約されています。

**pfnGetHandleDataCb**システム用に予約されています。

**pfnGetHandleParentCb**システム用に予約されています。

**pfnEnumHandleChildrenCb**システム用に予約されています。

**pfnNotifyInterruptCb**システム用に予約されています。

**pfnNotifyDpcCb**システム用に予約されています。

**pfnQueryVidPnInterfaceCb**システム用に予約されています。

**pfnGetCaptureAddressCb**システム用に予約されています。

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

 

 





