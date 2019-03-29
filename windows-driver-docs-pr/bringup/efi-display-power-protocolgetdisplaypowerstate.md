---
title: EFI_DISPLAY_POWER_PROTOCOL.GetDisplayPowerState
description: EFI_DISPLAY_POWER_PROTOCOL.GetDisplayPowerState
ms.assetid: 8c5fe55f-903e-4ef0-b3cf-8b764af767cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46d6f29f8c91834a95b7cdeb9a1aa1bf6c391e94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574874"
---
# <a name="efidisplaypowerprotocolgetdisplaypowerstate"></a>EFI\_表示\_POWER\_プロトコル。GetDisplayPowerState


現在の電源状態の表示とバックライトを返します。

## <a name="syntax"></a>構文


```cpp
typedef EFI_STATUS (EFIAPI * EFI_DISPLAY_POWER_GETDISPLAYPOWERSTATE) (
    IN EFI_DISPLAY_POWER_PROTOCOL *This,
    OUT EFI_DISPLAY_POWER_STATE *PowerState 
    );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
\[\]へのポインター、 [EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)インスタンス。

<a href="" id="powerstate"></a>*PowerState*  
\[out\]へのポインター、 [EFI\_表示\_POWER\_状態](efi-display-power-state.md)現在の電源状態を受信する値。

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
<td><p>関数が正常に返されます。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>パラメーターが無効です。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック
[EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)  



