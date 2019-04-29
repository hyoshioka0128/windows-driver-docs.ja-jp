---
title: EFI_RNG_PROTOCOL.GetInfo
description: EFI_RNG_PROTOCOL.GetInfo
ms.assetid: 11E9927B-8BC6-4B01-A12D-C75B636E3988
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5a73e42b9de694807312a0e018185969bfd512a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328002"
---
# <a name="efirngprotocolgetinfo"></a>EFI\_RNG\_プロトコル。GetInfo


EFI を実装するドライバーによってサポートされている RNG アルゴリズムに関する情報を返します\_RNG\_プロトコル。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI *EFI_RNG_GET_INFO) (
    IN  struct _EFI_RNG_PROTOCOL    *This,
    IN  OUT UINTN                   *RNGAlgorithmListSize,
    OUT EFI_RNG_ALGORITHM           *RNGAlgorithmList
    );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\]へのポインター、 [EFI\_RNG\_プロトコル](efi-rng-protocol.md)インスタンス。

<a href="" id="rngalgorithmlistsize"></a>*RNGAlgorithmListSize*  
\[入力、出力\]アルゴリズム数*RNGAlgorithmList*します。

<a href="" id="rngalgorithmlist"></a>*RNGAlgorithmList*  
\[out\]の一覧へのポインター [EFI\_RNG\_アルゴリズム](efi-display-power-state.md)RNG アルゴリズムを表す値。 各アルゴリズムは`sizeof(EFI_GUID)`バイト長。

## <a name="remarks"></a>注釈


EFI を実装するドライバー\_RNG\_プロトコルは、1 つまたは複数の RNG アルゴリズムをサポートできます。

によって返される値、 *RNGAlgorithmList*パラメーターは、同じドライバーを複数回呼び出す間で変更する必要があります。 最初のアルゴリズムの一覧では、ドライバーの既定のアルゴリズムです。

アルゴリズムの一覧が EFI を使用してこの関数によって割り当てられた\_ブート\_サービス -&gt;AllocatePool()、また、EFI を使用して、この一覧を解放する呼び出し元の責任\_ブート\_サービス&gt;FreePool() します。

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
<td><p>関数は、正常に RNG アルゴリズムの一覧を取得します。</p></td>
</tr>
<tr class="even">
<td><p>EFI_UNSUPPORTED</p></td>
<td><p>このドライバーでは、サービスがサポートされていません。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>ハードウェアまたはファームウェアのエラーのため、RNG アルゴリズムの一覧を取得できませんでした。</p></td>
</tr>
<tr class="even">
<td><p>EFI_OUT_OF_RESOURCES</p></td>
<td><p>ドライバーのメモリを割り当てることがない、 <em>RNGAlgorithmList</em>パラメーター。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




