---
title: EFI_USBFN_IO_PROTOCOL.StartController
description: EFI_USBFN_IO_PROTOCOL.StartController
ms.assetid: 431406c3-6b96-4815-a8a0-01100e8a5a5f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6053e93a7d9e47b20ec716513a4e50a7d596e991
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337685"
---
# <a name="efiusbfnioprotocolstartcontroller"></a>EFI\_USBFN\_IO\_プロトコル。StartController


**StartController**関数が必要な場合は、USB コント ローラーに電力を供給し、ハードウェアおよび内部データ構造体を初期化します。 ポートは、この関数によってアクティブ化されませんする必要があります。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_START_CONTROLLER) (
  IN EFI_USBFN_IO_PROTOCOL        *This
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

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
<td><p>関数が正常に返されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>パラメーターが無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


この関数は、以降のリビジョン 0x00010001 で利用可能、 **EFI\_USBFN\_IO\_プロトコル**します。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




