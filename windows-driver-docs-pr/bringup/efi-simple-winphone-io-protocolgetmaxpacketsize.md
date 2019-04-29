---
title: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.GetMaxPacketSize
description: EFI_SIMPLE_WINPHONE_IO_PROTOCOL.GetMaxPacketSize
ms.assetid: 8808bb5d-e00d-4b19-87ad-4a071a896e22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473395ba84360980f2a279e56a2a1b420fb3e21e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337792"
---
# <a name="efisimplewinphoneioprotocolgetmaxpacketsize"></a>EFI\_単純\_WINPHONE\_IO\_プロトコル。GetMaxPacketSize


**GetMaxPacketSize**関数は、1 つ格納できるバイトの最大数は、読み取りまたは書き込み操作を返します。

## <a name="syntax"></a>構文


```cpp
typedef 
EFI_STATUS 
(EFIAPI * EFI_SIMPLE_WINPHONE_IO_GET_MAXPACKET_SIZE) ( 
  IN EFI_SIMPLE_WINPHONE_IO_PROTOCOL    *This, 
  OUT UINTN                             *MaxPacketSize 
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_単純\_WINPHONE\_IO\_プロトコル インスタンス。

<a href="" id="maxpacketsize"></a>*この*  
最大値には、(バイト単位) パケットのサイズがサポートされています。

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
</tbody>
</table>

 

## <a name="remarks"></a>注釈


## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




