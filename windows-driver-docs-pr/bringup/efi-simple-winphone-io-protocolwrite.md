---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Write
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.Write
ms.assetid: 55475573-e904-4adc-91cf-62afe9e67927
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24ebe500efe1da3cc058369c84b341f1bbf7c0c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337759"
---
# <a name="efisimplewinphoneioprotocolwrite"></a>EFI\_単純\_WINPHONE\_IO\_プロトコル。書き込み


**書き込み**関数は、デバイスにデータを書き込みます。

この関数は、要求されたデータ量がデバイスに書き込まれるか、タイムアウトまでにブロックされます。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_SIMPLE_WINPHONE_IO_WRITE) (
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This,
  IN UINTN                              NumberOfBytesToWrite,
  IN OUT UINTN                          *NumberOfBytesWritten,
  IN VOID                               *Buffer
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_単純\_WINPHONE\_IO\_プロトコル インスタンス

<a href="" id="numberofbytestowrite"></a>*NumberOfBytesToWrite*  
デバイスに書き込むバイト数。

<a href="" id="numberofbyteswritten"></a>*NumberOfBytesWritten*  
(バイト単位) に実際に書き込まれたデータの量。

<a href="" id="buffer"></a>*バッファー*  
書き込むデータのバッファー。

## <a name="return-values"></a>戻り値


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

 

## <a name="remarks"></a>注釈


エラーが発生した場合、適切な状態コードで、転送を終了します。 場合は、実際には、デバイスに書き込まれたバイト数が返される**NumberOfBytesWritten**します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




