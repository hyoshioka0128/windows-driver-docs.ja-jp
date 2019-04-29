---
title: EFI_DISPLAY_POWER_PROTOCOL.SetDisplayPowerState
description: EFI_DISPLAY_POWER_PROTOCOL.SetDisplayPowerState
ms.assetid: ee638d05-4d0e-45b0-a733-73923a7c045a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7504bbe3f16cdd33fdd9f33803be203be0c0c5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328010"
---
# <a name="efidisplaypowerprotocolsetdisplaypowerstate"></a>EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState


ディスプレイおよびバックライト電源の状態を変更します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS (EFIAPI * EFI_DISPLAY_POWER_SETDISPLAYPOWERSTATE) (
    IN EFI_DISPLAY_POWER_PROTOCOL *This,
    IN EFI_DISPLAY_POWER_STATE PowerState 
    );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\]へのポインター、 [EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)インスタンス。

<a href="" id="powerstate"></a>*PowerState*  
\[\] 、 [EFI\_表示\_POWER\_状態](efi-display-power-state.md)を設定する新しい電源の状態を指定する値。

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
<td><p>表示とバックライトの両方の電源の状態を変更した後に正常に返される関数。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>パラメーターが正しくありません。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


この関数による影響はありません、画面またはバックライト以外の任意のハードウェア コンポーネントにします。

この関数は、エラー コードを返さずに冗長な呼び出しを許可する必要があります。 同じでは、この関数を複数回呼び出す*PowerState*引数は、成功を返す必要があります。 この関数の実装は、冗長な呼び出しを処理するときに、不要な処理を避ける必要があります。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック
[EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)  



