---
title: HS_HOST_ALLOCATE_MEMORY 関数
description: HS_HOST_ALLOCATE_MEMORY 関数は、呼び出し元によって指定されたメモリの量を返します。
ms.assetid: afa59680-d85b-4be5-8642-152ff653a0b0
keywords:
- Windows Vista 以降のドライバーをネットワーク (WINAPI HS_HOST_ALLOCATE_MEMORY) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 472bddbe033ffc6a6dd175a9c950c4e4216967f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349678"
---
# <a name="hshostallocatememory-function"></a>HS\_ホスト\_ALLOCATE\_メモリ関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ホスト\_ALLOCATE\_メモリ**関数が呼び出し元によって指定されたメモリの量を返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 (WINAPI *HS_HOST_ALLOCATE_MEMORY)(
  _In_  HANDLE                        hPluginContext,
  _In_  DWORD                         dwByteCount,
  _Out_ _bcount (dwByteCount) LPVOID* ppvBuffer
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
この関数を呼び出すプラグインのコンテキスト ハンドル。

*dwByteCount* \[in\]  
割り当てるメモリの量。

*ppvBuffer* \[out\]  
割り当てられたメモリを格納しているバッファーへのポインター。

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

 

 




