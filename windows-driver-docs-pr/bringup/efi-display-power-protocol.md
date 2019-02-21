---
title: EFI_DISPLAY_POWER_PROTOCOL
description: EFI_DISPLAY_POWER_PROTOCOL
ms.assetid: 61ccf856-7e0b-4f1b-9be9-7b8a31339a6b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 646406e0af3a813e986c3d804f64f279bff9f668
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553182"
---
# <a name="efidisplaypowerprotocol"></a>EFI\_表示\_POWER\_プロトコル


このプロトコルには、UEFI バッテリの充電 UEFI 環境の中に指定されたアイドル期間の後、画面をオフにするアプリケーションを充電ができます。

## <a name="syntax"></a>構文


```cpp
#define EFI_DISPLAY_POWER_PROTOCOL_GUID \
  {0xf352021d, 0x9593, 0x4432, {0xbf, 0x4, 0x67, 0xb9, 0xf3, 0xb7, 0x60, 0x8};

typedef struct _EFI_DISPLAY_POWER_PROTOCOL {  
    UINT32                                    Revision;  
    EFI_DISPLAY_POWER_SETDISPLAYPOWERSTATE    SetDisplayPowerState;  
    EFI_DISPLAY_POWER_GETDISPLAYPOWERSTATE    GetDisplayPowerState;  
} EFI_DISPLAY_POWER_PROTOCOL;
```

## <a name="members"></a>Members


<a href="" id="revision"></a>**リビジョン**  
リビジョン、 **EFI\_表示\_POWER\_プロトコル**準拠します。 すべての将来のリビジョンは、旧バージョンと互換性のあるである必要があります。 場合は、今後のバージョンは旧バージョンと互換性のある、別の GUID を使用する必要があります。

現在のリビジョンは 0x00010000 です。 リビジョンに設定してください 0x00010000、ファームウェアによってこの場合のリビジョン、 **EFI\_バッテリ\_充電中\_プロトコル**ファームウェアでサポートされています。

<a href="" id="setdisplaypowerstate"></a>**SetDisplayPowerState**  
ディスプレイおよびバックライト電源の状態を変更します。 詳細については、次を参照してください。 [EFI\_表示\_POWER\_プロトコル。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)します。

<a href="" id="getdisplaypowerstate"></a>**GetDisplayPowerState**  
現在の電源状態の表示とバックライトを返します。 詳細については、次を参照してください。 [EFI\_表示\_POWER\_プロトコル。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




