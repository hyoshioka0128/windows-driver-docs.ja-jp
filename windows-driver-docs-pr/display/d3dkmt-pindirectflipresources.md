---
title: D3DKMT\_PINDIRECTFLIPRESOURCES 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: c5c79876-a9b5-44fa-9545-3995118520d0
keywords:
- D3DKMT_PINDIRECTFLIPRESOURCES 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_PINDIRECTFLIPRESOURCES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 168cfc9304dd97130ff29ab6cd9d75a39e664db7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379736"
---
# <a name="d3dkmtpindirectflipresources-structure"></a>D3DKMT\_PINDIRECTFLIPRESOURCES 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_PINDIRECTFLIPRESOURCES {
  D3DKMT_HANDLE hDevice;
  UINT          ResourceCount;
  D3DKMT_HANDLE *pResourceList;
} D3DKMT_PINDIRECTFLIPRESOURCES;
```

<a name="members"></a>メンバー
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

 

 





