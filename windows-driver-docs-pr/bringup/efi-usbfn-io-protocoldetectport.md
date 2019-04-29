---
title: EFI_USBFN_IO_PROTOCOL.DetectPort
description: EFI_USBFN_IO_PROTOCOL.DetectPort
ms.assetid: 66f7500e-e075-495b-9ce0-aed2aa11f66a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 815b857212f225c7da8e9a87880d5333829a85ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337688"
---
# <a name="efiusbfnioprotocoldetectport"></a>EFI\_USBFN\_IO\_プロトコル。DetectPort


**DetectPort**関数は、USB ポートに接続されたデバイスの種類を返します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_DETECT_PORT) (
  IN EFI_USBFN_IO_PROTOCOL   *This,
  OUT EFI_USBFN_PORT_TYPE    *PortType
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="porttype"></a>*PortType*  
A [EFI\_USBFN\_ポート\_型](efi-usbfn-port-type.md)列挙型を示す、USB ポートの種類。

## <a name="return-values"></a>戻り値


この関数は、次の値を返します。

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

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




