---
title: EFI_USBFN_IO_PROTOCOL.GetVendorIdProductId
description: EFI_USBFN_IO_PROTOCOL.GetVendorIdProductId
ms.assetid: 78dbc589-3ffd-4ee2-9d80-4570b3b20b2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc95119621882735c518b36e23b6c1b4affd20a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530394"
---
# <a name="efiusbfnioprotocolgetvendoridproductid"></a>EFI\_USBFN\_IO\_プロトコル。GetVendorIdProductId


**GetVendorIdProductId**ベンダー id とデバイスの製品 id を返す関数。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_VENDOR_ID_PRODUCT_ID) (
  IN EFI_USBFN_IO_PROTOCOL      *This,
  OUT UINT16                    *Vid,
  OUT UINT16                    *Pid
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="vid"></a>*Vid*  
デバイスの返された仕入先 id。 仕入先 Id (, 試聴) を割り当てられ、USB によって管理される、および仕入先の会社が所有する 16 ビットの数値の場合。

<a href="" id="pid"></a>*pid*  
デバイスの返された製品 id。 製品 Id (Pid) は、自由に、各仕入先によって割り当てられた 16 ビットの数値です。

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
<td><p><strong>EFI_NOT_FOUND</strong></p></td>
<td><p>VID または PID を返すことができません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




