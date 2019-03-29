---
title: EFI_USBFN_IO_PROTOCOL.GetEndpointPolicy
description: EFI_USBFN_IO_PROTOCOL.GetEndpointPolicy
ms.assetid: 143ee448-2c29-46f4-b62c-6429a4a1d890
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ad5c2af7349738995cb17a4ff1e25b754ff831b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571626"
---
# <a name="efiusbfnioprotocolgetendpointpolicy"></a>EFI\_USBFN\_IO\_プロトコル。GetEndpointPolicy


**GetEndpointPolicy**関数は、指定したコントロール以外のエンドポイントの構成ポリシーを取得します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_GET_ENDPOINT_POLICY) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN EFI_USBFN_POLICY_TYPE        PolicyType,
  IN OUT UINTN                    BufferSize,
  IN OUT VOID                     *Buffer
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
ポリシーの種類、ユーザーが指定されたコントロール以外のエンドポイントを取得しようとしています。 詳細については、次を参照してください。 [EFI\_USBFN\_ポリシー\_型](efi-usbfn-policy-type.md)します。

<a href="" id="buffersize"></a>*BufferSize*  
入力のサイズ*バッファー* (バイト単位)。 出力に、によって返されるデータの量*バッファー* (バイト単位)。

<a href="" id="buffer"></a>*バッファー*  
要求されたエンドポイントのポリシー値を返すバッファーへのポインター。 ポリシーの種類のサイズ要件の詳細については、次を参照してください。 [EFI\_USBFN\_ポリシー\_型](efi-usbfn-policy-type.md)します。

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
<tr class="odd">
<td><p><strong>EFI_BUFFER_TOO_SMALL</strong></p></td>
<td><p>指定のバッファーが要求されたポリシーの値を保持するのに十分な大きさではありません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


この関数の呼び出し元の制限はありません。 この関数は、以降のリビジョン 0x00010001 で利用可能、 **EFI\_USBFN\_IO\_プロトコル**します。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




