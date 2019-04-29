---
title: DEVPROP_TYPE_EMPTY
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_EMPTY 識別子は、プロパティが存在しないことを示す特殊な基本データ型識別子を表します。
ms.assetid: 23d48659-e512-4557-a78b-d3afca7020a3
keywords:
- DEVPROP_TYPE_EMPTY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_EMPTY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0defffbc2d4077efcefdbb95695610d0e92155d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335243"
---
# <a name="devproptypeempty"></a>DEVPROP_TYPE_EMPTY


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_EMPTY 識別子は、プロパティが存在しないことを示す特殊な基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

プロパティを削除するのにデバイスのプロパティ関数でこの基本データ型識別子を使用します。

デバイスのプロパティ関数は、この基本データ型識別子を返します、プロパティは存在しません。

**DEVPROP_TYPE_EMPTY**プロパティ データ型の修飾子と組み合わせて使用できない[ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)または[ **DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md).

### <a name="deleting-a-property"></a>プロパティを削除します。

プロパティを削除するには、対応する SetupDiSet を呼び出す*Xxx*プロパティ関数とセットと関数パラメーターに依存します。

-   設定、 *PropertyType* DEVPROP_TYPE_EMPTY、パラメーター、 *PropertyBuffer*パラメーターを**NULL**、および*PropertyBufferSize*パラメーターを 0 にします。

-   プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

DEVPROP_TYPE_EMPTY は存在しないプロパティを削除する試行で使用する場合は、削除操作は失敗、および呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) ERROR_NOT_FOUND が返されます。

### <a name="retrieving-a-property-that-does-not-exist"></a>存在しないプロパティを取得します。

呼び出し、SetupDiGet*Xxx*プロパティ関数が存在しないデバイス プロパティは失敗し、取得、および後続の呼び出しを試行する[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) ERROR_NOT_FOUND が返されます。 呼び出された SetupAPI プロパティ関数の設定、 \* *PropertyType* DEVPROP_TYPE_EMPTY パラメーター。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





