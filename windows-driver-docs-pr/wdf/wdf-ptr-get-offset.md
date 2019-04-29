---
title: WDF_PTR_GET_OFFSET macro
description: WDF_PTR_GET_OFFSET マクロは、別のアドレスからアドレスを減算し、結果として得られるオフセット値を返します。
ms.assetid: b5159207-ba5c-4924-a06e-725ccd3c8a12
keywords:
- WDF_PTR_GET_OFFSET macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1782a7545ace74a23948ebd19b7bad579b04542
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390831"
---
# <a name="wdfptrgetoffset-macro"></a>WDF_PTR_GET_OFFSET macro


**WDF_PTR_GET_OFFSET**マクロは、別のアドレスからアドレスを減算し、結果として得られるオフセット値を返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
size_t WDF_PTR_GET_OFFSET(
    _base,
    _addr
);
```

<a name="parameters"></a>パラメーター
----------

*_base*   
開始アドレスから減算する値を指定します。

*_addr*   
開始アドレスを指定します。

<a name="return-value"></a>戻り値
------------

2 つの指定されたアドレス間のオフセットを返します。

<a name="remarks"></a>注釈
-------

マクロの定義は次のとおりです。

```ManagedCPlusPlus
#define WDF_PTR_GET_OFFSET(_base, _addr) \
        (size_t) (((PUCHAR) _addr) - ((PUCHAR) _base))
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td><p>最小 KMDF バージョン</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfcore.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>

 

 






