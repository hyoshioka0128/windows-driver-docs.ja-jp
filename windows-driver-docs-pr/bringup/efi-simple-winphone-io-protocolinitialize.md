---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Initialize
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Initialize
ms.assetid: e27ed767-7854-4b2f-8043-35c39357eee4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d97671cbdffee53a43ac7fce5e85d4d6a36ad1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337800"
---
# <a name="efisimplewinphoneioprotocolinitialize"></a>EFI\_単純\_WINPHONE\_IO\_プロトコル。初期化します。


**初期化**関数は指定した秒数のホスト コンピューターからの接続を待機します。 有効な接続を行わない場合**EFI\_タイムアウト**はエラー状態として返されます。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS(EFIAPI * EFI_SIMPLE_WINPHONE_IO_INITIALIZE) 
(
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              ConnectionTimeout,
  IN UINTN                              ReadWriteTimeout
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_単純\_WINPHONE\_IO\_プロトコル インスタンス。

<a href="" id="connectiontimeout"></a>*ConnectionTimeout*  
ホスト コンピューターからの接続を待機するミリ秒数。

<a href="" id="readwritetimeout"></a>*ReadWriteTimeout*  
読み取りの待機操作と書き込み操作を完了する時間 (ミリ秒) の数。

## <a name="return-values"></a>戻り値


関数は、次の値のいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EFI_SUCCESS</strong></p></td>
<td><p>正常に返される関数</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>パラメーターが無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理デバイスがビジー状態か、この要求を処理する準備ができていません</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_TIMEOUT</strong></p></td>
<td><p>接続を確立する前にタイムアウトが発生しました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




