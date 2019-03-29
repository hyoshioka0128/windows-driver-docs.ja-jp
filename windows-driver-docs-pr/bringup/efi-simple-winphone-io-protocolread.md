---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Read
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Read
ms.assetid: 9b5525a4-d98c-4328-8ebe-55ede53befca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b71ff27f2e13acb8a3c6076382658f75e9bcd4b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573018"
---
# <a name="efisimplewinphoneioprotocolread"></a>EFI\_単純\_WINPHONE\_IO\_プロトコル。読み取り


**読み取り**関数は、デバイスからデータを読み取ります。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_SIMPLE_WINPHONE_IO_READ) (
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              NumberOfBytesToRead,
  IN OUT UINTN                          *NumberOfBytesRead,
  OUT VOID                              *Buffer
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_単純\_WINPHONE\_IO\_プロトコル インスタンス。

<a href="" id="numberofbytestoread"></a>*NumberOfBytesToRead*  
読み取られるバイトの最大数。

<a href="" id="numberofbytesread"></a>*NumberOfBytesRead*  
バッファーのバイト単位で返されるデータの量

<a href="" id="buffer"></a>*バッファー*  
データを返すバッファー。

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
<tr class="even">
<td><p><strong>EFI_NO_RESPONSE</strong></p></td>
<td><p>ホストへの接続が存在しないかが終了しました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


この関数は、要求されたデータ量があるか、タイムアウトまでにブロックされます。

エラーが発生した場合、以上のバイトを読み取るし、適切な状態コードが返されます。 場合は、実際に読み取られたバイト数が返される**NumberOfBytesRead**します。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




