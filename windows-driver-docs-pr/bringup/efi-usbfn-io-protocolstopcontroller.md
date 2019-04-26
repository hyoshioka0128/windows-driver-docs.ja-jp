---
title: EFI_USBFN_IO_PROTOCOL.StopController
description: EFI_USBFN_IO_PROTOCOL.StopController
ms.assetid: 531fd280-bcb1-4b6f-a2fa-9052318171b3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 366b30016650084b171e94321117fae20d6eab0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337690"
---
# <a name="efiusbfnioprotocolstopcontroller"></a>EFI\_USBFN\_IO\_プロトコル。StopController


**StopController**関数は、必要に応じて、実行/ストップ ビットと電源オフ、USB コント ローラーをリセットすることで、ハードウェア デバイスを無効にします。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_STOP_CONTROLLER) (
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

 

 




