---
title: OUTPUTDUPL\_コンテキスト\_デバッグ\_情報構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 9b8915a2-e62e-474a-ac03-199ce6d252c2
keywords:
- OUTPUTDUPL_CONTEXT_DEBUG_INFO 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- OUTPUTDUPL_CONTEXT_DEBUG_INFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bc91f429563af15195dd15a557f472102c518928
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358344"
---
# <a name="outputduplcontextdebuginfo-structure"></a>OUTPUTDUPL\_コンテキスト\_デバッグ\_情報構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _OUTPUTDUPL_CONTEXT_DEBUG_INFO {
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS Status;
  HANDLE                          ProcessID;
  UINT32                          AccumulatedPresents;
  LARGE_INTEGER                   LastPresentTime;
  LARGE_INTEGER                   LastMouseTime;
  CHAR                            ProcessName[DXGK_DIAG_PROCESS_NAME_LENGTH];
} OUTPUTDUPL_CONTEXT_DEBUG_INFO;
```

<a name="members"></a>メンバー
-------

**ステータス**

**プロセス Id**

**AccumulatedPresents**

**LastPresentTime**

**LastMouseTime**

**ProcessName**

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

 

 





