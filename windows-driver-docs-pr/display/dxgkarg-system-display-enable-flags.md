---
title: DXGKARG\_システム\_表示\_を有効にする\_フラグ構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: f23d6692-4c9d-48eb-8d7f-ef70334494b1
keywords:
- DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS 構造体のディスプレイ デバイス
- PDXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS 構造体ポインター ディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3fcae06de43c0499f557e3793f0066d41a63328d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572643"
---
# <a name="dxgkargsystemdisplayenableflags-structure"></a>DXGKARG\_システム\_表示\_を有効にする\_フラグ構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS {
  union {
    struct {
      UINT Reserved  :32;
    };
    UINT   Value;
  };
} DXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS, *PDXGKARG_SYSTEM_DISPLAY_ENABLE_FLAGS;
```

<a name="members"></a>メンバー
-------

**予約済み**システム用に予約されています。

**値**システム用に予約されています。

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
<td align="left">Dispmprt.h</td>
</tr>
</tbody>
</table>

 

 





