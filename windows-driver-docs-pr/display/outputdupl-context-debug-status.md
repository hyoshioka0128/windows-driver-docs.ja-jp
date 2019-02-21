---
title: OUTPUTDUPL\_コンテキスト\_デバッグ\_状態の列挙型
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 3720b101-cac4-4f81-ae71-088ab03f8756
keywords:
- OUTPUTDUPL_CONTEXT_DEBUG_STATUS 列挙ディスプレイ デバイス
topic_type:
- apiref
api_name:
- OUTPUTDUPL_CONTEXT_DEBUG_STATUS
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c8ed67cc886550c192e40629defd629c82a44901
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556895"
---
# <a name="outputduplcontextdebugstatus-enumeration"></a>OUTPUTDUPL\_コンテキスト\_デバッグ\_状態の列挙型


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _OUTPUTDUPL_CONTEXT_DEBUG_STATUS {
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_INACTIVE         = 0,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_ACTIVE           = 1,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_PENDING_DESTROY  = 2,
  OUTPUTDUPL_CONTEXT_DEBUG_STATUS_FORCE_UINT32     = 0xffffffff
} OUTPUTDUPL_CONTEXT_DEBUG_STATUS;
```

<a name="constants"></a>定数
---------

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_INACTIVE"></span><span id="outputdupl_context_debug_status_inactive"></span>**OUTPUTDUPL\_コンテキスト\_デバッグ\_状態\_非アクティブ**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_ACTIVE"></span><span id="outputdupl_context_debug_status_active"></span>**OUTPUTDUPL\_コンテキスト\_デバッグ\_状態\_ACTIVE**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_PENDING_DESTROY"></span><span id="outputdupl_context_debug_status_pending_destroy"></span>**OUTPUTDUPL\_コンテキスト\_デバッグ\_状態\_PENDING\_破棄**

<span id="OUTPUTDUPL_CONTEXT_DEBUG_STATUS_FORCE_UINT32"></span><span id="outputdupl_context_debug_status_force_uint32"></span>**OUTPUTDUPL\_CONTEXT\_DEBUG\_STATUS\_FORCE\_UINT32**

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

 

 





