---
title: EFI_RNG_PROTOCOL.GetRNG
description: EFI_RNG_PROTOCOL.GetRNG
ms.assetid: 5C2E0C8F-FF3A-4F57-BC28-3BC540852CB0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0654078e31d852be913d2325104884fe1fd7f708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327996"
---
# <a name="efirngprotocolgetrng"></a>EFI\_RNG\_プロトコル。GetRNG


ランダムな数の生成 (RNG) 値を取得します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS (EFIAPI *EFI_RNG_GET_RNG) (
    IN  struct _EFI_RNG_PROTOCOL    *This,
    IN  EFI_RNG_ALGORITHM           *RNGAlgorithm, OPTIONAL
    IN  UINTN                       RNGValueLength,
    OUT UINT8                       *RNGValue
    );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\]へのポインター、 [EFI\_RNG\_プロトコル](efi-rng-protocol.md)インスタンス。

<a href="" id="rngalgorithm"></a>*RNGAlgorithm*  
\[\] EFI へのポインター\_RNG\_アルゴリズムを使用する RNG アルゴリズムを識別します。 このパラメーターが NULL の場合は、ドライバーでサポートされている既定のアルゴリズムが使用されます。

<a href="" id="rngvaluelength"></a>*RNGValueLength*  
\[\]によって返されるバッファーの長さをバイト単位で*RNGValue*します。

<a href="" id="rngvalue"></a>*RNGValue*  
\[\] RNG 値を格納するバッファーへのポインター。 EFI を使用してこの関数によって値が割り当てられた\_ブート\_サービス -&gt;AllocatePool()、また、EFI を使用してこのメモリを解放する呼び出し元の責任\_ブート\_サービス&gt;FreePool() します。

## <a name="remarks"></a>注釈


最小サイズ*RNGValue*は 32 バイトです。

## <a name="return-value"></a>戻り値


次のステータス コードのいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>関数には、RNG 値を正常に返されます。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p><em>RNGAlgorithm</em>が NULL の場合、いくつかのアルゴリズムが可能です。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_UNSUPPORTED</p></td>
<td><p>指定されたアルゴリズム<em>RNGAlgorithm</em>は、このドライバーではサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>RNG 値をハードウェアとファームウェアのエラーのため取得できませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_NOT_READY</p></td>
<td><p>ないのに十分なエントロピー データ。</p></td>
</tr>
<tr class="even">
<td><p>EFI_OUT_OF_RESOURCES</p></td>
<td><p>ドライバーは RNG 値のメモリを割り当てられませんが。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




