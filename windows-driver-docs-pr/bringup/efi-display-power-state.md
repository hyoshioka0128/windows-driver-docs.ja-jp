---
title: EFI_DISPLAY_POWER_STATE
description: EFI_DISPLAY_POWER_STATE
ms.assetid: b4b0980b-db87-44e8-842c-afce0c8df0a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2a9230c4286efe8a39a2a3f7fdbee8c2a8cf327
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528729"
---
# <a name="efidisplaypowerstate"></a>EFI\_表示\_POWER\_状態


この列挙体は、表示、バックライトの充電状態を表します。 この列挙型のパラメーターは、 [EFI\_表示\_POWER\_プロトコル。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)と[EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)関数。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_DISPLAY_POWER_STATE {  
    EfiDisplayPowerStateUnknown = 0,  
    EfiDisplayPowerStateOff,  
    EfiDisplayPowerStateMaximum,  
} EFI_DISPLAY_POWER_STATE;
```

## <a name="elements"></a>要素


<a href="" id="efidisplaypowerstateunknown"></a>EfiDisplayPowerStateUnknown  
電源の状態が初期化されていません。 この値は、変数の初期化にのみ使用できます。渡されるまたはいずれかによって返されることはできません[EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)関数。

<a href="" id="efidisplaypowerstateoff"></a>EfiDisplayPowerStateOff  
使用すると[EFI\_表示\_POWER\_プロトコル。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)ディスプレイやバックライトに電源がになっていることを示します。 使用すると[EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)電源、ディスプレイとバックライトをオフにします。

<a href="" id="efidisplaypowerstatemaximum"></a>EfiDisplayPowerStateMaximum  
使用すると[EFI\_表示\_POWER\_プロトコル。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)表示とバックライトが全機能を使用することを示します。 使用すると[EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)ディスプレイやバックライトに完全な電源をオンにします。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

## <a name="related-topics"></a>関連トピック
[EFI\_表示\_POWER\_プロトコル](efi-display-power-protocol.md)  



