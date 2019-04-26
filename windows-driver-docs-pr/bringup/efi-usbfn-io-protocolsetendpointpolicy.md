---
title: EFI_USBFN_IO_PROTOCOL.SetEndpointPolicy
description: EFI_USBFN_IO_PROTOCOL.SetEndpointPolicy
ms.assetid: d7ab0529-1925-47b5-9706-2e6288a6a5cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1365e0454195d6476a69e430325e4212770abc56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337687"
---
# <a name="efiusbfnioprotocolsetendpointpolicy"></a>EFI\_USBFN\_IO\_プロトコル。SetEndpointPolicy


**SetEndpointPolicy**関数は、指定したコントロール以外のエンドポイントの構成ポリシーを設定します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_SET_ENDPOINT_POLICY) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN EFI_USBFN_POLICY_TYPE        PolicyType,
  IN UINTN                        BufferSize,
  IN VOID                         *Buffer
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="endpointindex"></a>*EndpointIndex*  
ポリシーで設定が必要のあるコントロール以外のエンドポイントを示します。

<a href="" id="direction"></a>*方向*  
エンドポイントの方向です。 詳細については、次を参照してください。 [EFI\_USBFN\_エンドポイント\_方向](efi-usbfn-endpoint-direction.md)します。

<a href="" id="policytype"></a>*PolicyType*  
ポリシーの種類、ユーザーが指定されたコントロール以外のエンドポイントを設定しようとしています。 詳細については、次を参照してください。 [EFI\_USBFN\_ポリシー\_型](efi-usbfn-policy-type.md)します。

<a href="" id="buffersize"></a>*BufferSize*  
サイズ*バッファー* (バイト単位)。

<a href="" id="buffer"></a>*バッファー*  
新しいエンドポイント ポリシーの値を格納しているバッファーへのポインター。 ポリシーの種類のサイズ要件の詳細については、次を参照してください。 [EFI\_USBFN\_ポリシー\_型](efi-usbfn-policy-type.md)します。

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
<tr class="even">
<td><p><strong>EFI_UNSUPPORTED</strong></p></td>
<td><p>このポリシーの値を変更することはできません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


この関数は前にのみ呼び出すことができます[EFI\_USBFN\_IO\_プロトコル。StartController](efi-usbfn-io-protocolstartcontroller.md)後または[EFI\_USBFN\_IO\_プロトコル。StopController](efi-usbfn-io-protocolstopcontroller.md)が呼び出されました。 この関数は、以降のリビジョン 0x00010001 で利用可能、 **EFI\_USBFN\_IO\_プロトコル**します。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




