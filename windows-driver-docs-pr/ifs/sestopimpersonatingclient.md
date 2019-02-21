---
title: SeStopImpersonatingClient ルーチン
description: SeStopImpersonatingClient ルーチンでは、ユーザーの偽装を呼び出し元のスレッドを終了します。
ms.assetid: 1aab384b-919c-4709-9ceb-66616c622714
keywords:
- SeStopImpersonatingClient ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 2dfd01a7cb7c1768eef553b4137c3ddf763ee1fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558697"
---
# <a name="sestopimpersonatingclient-routine"></a>SeStopImpersonatingClient ルーチン


**SeStopImpersonatingClient**ルーチンがユーザーの偽装を呼び出し元のスレッドを終了します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID SeStopImpersonatingClient(void);
```

<a name="parameters"></a>パラメーター
----------

このルーチンには、パラメーターがありません。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

サーバーのスレッドは呼び出すことによってユーザーを偽装することができます、 [ **SeImpersonateClientEx** ](https://msdn.microsoft.com/library/windows/hardware/ff556659)ルーチン。 スレッドが終了すると、ユーザーの偽装を呼び出し、 **SeStopImpersonatingClient**権限借用の終了ルーチン。

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
<td align="left"><p>Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SeImpersonateClientEx**](https://msdn.microsoft.com/library/windows/hardware/ff556659)

 

 






