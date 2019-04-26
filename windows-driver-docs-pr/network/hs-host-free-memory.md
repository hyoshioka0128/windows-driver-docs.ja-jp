---
title: HS_HOST_FREE_MEMORY 関数
description: HS_HOST_FREE_MEMORY 関数は、HS_HOST_ALLOCATE_MEMORY への呼び出しによって以前に割り当てられたメモリを解放します。
ms.assetid: 2090ecf8-e1d5-4410-acbf-1b97f418e185
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef VOID (WINAPI HS_HOST_FREE_MEMORY) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9d9e8a423787f49758a4047adba566420283880
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349666"
---
# <a name="hshostfreememory-function"></a>HS\_ホスト\_FREE\_メモリ関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ホスト\_FREE\_メモリ**関数への呼び出しによって以前に割り当てられたメモリを解放する[ **HS\_ホスト\_割り当て\_メモリ**](hs-host-allocate-memory.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef VOID (WINAPI *HS_HOST_FREE_MEMORY)(
  _In_     HANDLE hPluginContext,
  _In_opt_ LPVOID pvBuffer
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
この関数を呼び出すプラグインのコンテキスト ハンドル。

*pvBuffer* \[で、省略可能\]  
メモリ バッファーへのポインター。

<a name="return-value"></a>戻り値
------------

この関数は、ホストと通信するようにプラグインによって呼び出され、値は返されません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**HS\_ホスト\_ALLOCATE\_メモリ**](hs-host-allocate-memory.md)

 

 




