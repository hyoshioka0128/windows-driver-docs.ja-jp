---
title: SeStopImpersonatingClient ルーチン
description: SeStopImpersonatingClient ルーチンは、ユーザーの呼び出し元スレッドの偽装を終了します。
ms.assetid: 1aab384b-919c-4709-9ceb-66616c622714
keywords:
- SeStopImpersonatingClient ルーチンのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- SeStopImpersonatingClient
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa5ff5053b13dfbcbd4e7740c33e621c2a245f95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840966"
---
# <a name="sestopimpersonatingclient-routine"></a>SeStopImpersonatingClient ルーチン


**SeStopImpersonatingClient**ルーチンは、ユーザーの呼び出し元スレッドの偽装を終了します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID SeStopImpersonatingClient(void);
```

<a name="parameters"></a>パラメーター
----------

このルーチンにはパラメーターがありません。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

サーバースレッドは、 [**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)ルーチンを呼び出すことによってユーザーの権限を借用できます。 スレッドがユーザーの偽装を完了すると、 **SeStopImpersonatingClient**ルーチンが呼び出され、偽装が終了します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)

 

 






