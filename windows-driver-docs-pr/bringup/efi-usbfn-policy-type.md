---
title: EFI_USBFN_POLICY_TYPE
description: EFI_USBFN_POLICY_TYPE
ms.assetid: 51f615d4-a226-45d5-b5e9-fea4859640a9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fba94c165161fe8a6131cd74ed5402d5e322552
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560790"
---
# <a name="efiusbfnpolicytype"></a>EFI\_USBFN\_ポリシー\_型


**EFI\_USBFN\_ポリシー\_型**列挙には、エンドポイントの種類を示すために使用される値が含まれています。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USBFN_POLICY_TYPE{
  EfiUsbPolicyUndefined = 0, 
  EfiUsbPolicyMaxTransactionSize, 
  EfiUsbPolicyZeroLengthTerminationSupport, 
  EfiUsbPolicyZeroLengthTermination
} EFI_USBFN_POLICY_TYPE;
```

## <a name="constants"></a>定数


<a href="" id="efiusbpolicyundefined"></a>**EfiUsbPolicyUndefined**  
無効なポリシー値ドライバーの境界を越えて使用することはありません。 使用する場合、呼び出し先関数が成功状態コードを返すことはありません必要があります。

<a href="" id="efiusbpolicymaxtransactionsize"></a>**EfiUsbPolicyMaxTransactionSize**  
このポリシーは、読み取り専用です。 使用すると[EFI\_USBFN\_IO\_プロトコル。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)、コント ローラーでサポートされている最大の 1 つのトランザクション (サービスのエンドポイントに配信) のサイズが返されます。 呼び出すことによって取得できる最大転送サイズ以上する必要があります[EFI\_USBFN\_IO\_プロトコル。GetMaxTransferSize](efi-usbfn-io-protocolgetmaxtransfersize.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>GetEndpointPolicy</th>
<th>SetEndpointPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BufferSize</em></p></td>
<td><p>4 バイト、sizeof(UINT32)</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>戻り値の状態</p></td>
<td><p>EFI_STATUS</p></td>
<td><p>EFI_UNSUPPORTED</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="efiusbpolicyzerolengthterminationsupport"></a>**EfiUsbPolicyZeroLengthTerminationSupport**  
このポリシーは、読み取り専用です。 使用すると[EFI\_USBFN\_IO\_プロトコル。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)、USB コント ローラーのハードウェアが自動的に転送サイズは USB のパケットの最大サイズの倍数にするときに長さ 0 のパケットを処理できる場合は、TRUE が返されます。コント ローラーのハードウェアでは、このようなシナリオはサポートされていない場合は、FALSE が返されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>GetEndpointPolicy</th>
<th>SetEndpointPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BufferSize</em></p></td>
<td><p>1 バイト、sizeof(BOOLEAN)</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>戻り値の状態</p></td>
<td><p>EFI_STATUS</p></td>
<td><p>EFI_UNSUPPORTED</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="efiusbpolicyzerolengthtermination"></a>**EfiUsbPolicyZeroLengthTermination**  
使用すると[EFI\_USBFN\_IO\_プロトコル。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)、USB コント ローラーのハードウェアが自動的に転送サイズが USB 最大パケット サイズの倍数である場合、長さ 0 のパケットを処理するために構成されている場合、TRUE が返されますこのようなシナリオをサポートするために、コント ローラーのハードウェアが構成されていない場合は、FALSE が返されます。

[EFI\_USBFN\_IO\_プロトコル。SetEndpointPolicy](efi-usbfn-io-protocolsetendpointpolicy.md) USB コント ローラーのハードウェアが長さ 0 のパケットを自動終了をサポートできる場合のみ、この種類のポリシーを受け入れることができます。 指定したエンドポイントの長さ 0 の終了を処理するために、コント ローラーを構成する必要がありますこの値が TRUE に設定されている場合FALSE 値をこのような方法で、コント ローラーを構成しません。

コント ローラーのハードウェアが長さ 0 の自動終了をサポートできる場合であっても、既定の構成はできません。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>GetEndpointPolicy</th>
<th>SetEndpointPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BufferSize</em></p></td>
<td><p>1 バイト、sizeof(BOOLEAN)</p></td>
<td><p>1 バイト、sizeof(BOOLEAN)</p></td>
</tr>
<tr class="even">
<td><p>戻り値の状態</p></td>
<td><p>EFI_STATUS</p></td>
<td><p>EFI_STATUS</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




