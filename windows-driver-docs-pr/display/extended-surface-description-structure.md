---
title: 拡張サーフェス情報構造
description: 拡張サーフェス情報構造
ms.assetid: 51936b15-590c-4113-a393-1a8306c24e7f
keywords:
- 描画サーフェイス機能 WDK DirectDraw、構造体の説明を拡張します。
- DirectDraw 拡張サーフェイス機能 WDK Windows 2000 の表示、構造体の説明
- 拡張セキュリティ機能 WDK DirectDraw、構造体の説明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9cd2cd0aa2411bc64391d41426f6fad9acaea00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381854"
---
# <a name="extended-surface-description-structure"></a>拡張サーフェス情報構造


## <span id="ddk_extended_surface_description_structure_gg"></span><span id="DDK_EXTENDED_SURFACE_DESCRIPTION_STRUCTURE_GG"></span>


拡張の DirectDraw surface 説明構造[ **DDSURFACEDESC2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))と同じですが、 [ **DDSURFACEDESC** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))構造体点を除いてへのポインター、 [ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))へのポインターに置き換えられました構造体、構造体の最後に、 [ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))構造体。

データのブロック、 [ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))と[ *DdCanCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))ドライバー呼び出しが、DDSURFACEDESC へのポインターを含む構造体。 DirectX 6.0 以降では、これらのポインターが実際に DDSURFACEDESC2 構造体を指す、ポインターのまま LPDDSURFACEDESC として型指定された場合でも。 調べることができますが、ドライバーが選択した場合、 **dwSize**のメンバー、 [ **DDSURFACEDESC** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550339(v=vs.85))ポインター、それによってポインターが実際を指すかどうかを決定し、 [ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))構造体。 ドライバーは、前 DirectX 6.0 のインストールで実行する必要があります、この確認を行うする必要があります。

返されるサイズが sizeof(DDSURFACEDESC2) の場合は、ドライバーが調べることができますし、 **dwCaps2**、 **dwCaps3**、および**dwCaps4**のメンバー、 [ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))構造体。

 

 





