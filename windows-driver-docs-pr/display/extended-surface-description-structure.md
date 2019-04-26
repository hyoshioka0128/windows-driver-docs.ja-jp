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
ms.openlocfilehash: 895c160190a21daacc954a0c2e71fe5285a7a786
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353595"
---
# <a name="extended-surface-description-structure"></a>拡張サーフェス情報構造


## <span id="ddk_extended_surface_description_structure_gg"></span><span id="DDK_EXTENDED_SURFACE_DESCRIPTION_STRUCTURE_GG"></span>


拡張の DirectDraw surface 説明構造[ **DDSURFACEDESC2**](https://msdn.microsoft.com/library/windows/hardware/ff550340)と同じですが、 [ **DDSURFACEDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff550339)構造体点を除いてへのポインター、 [ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)へのポインターに置き換えられました構造体、構造体の最後に、 [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)構造体。

データのブロック、 [ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)と[ *DdCanCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549213)ドライバー呼び出しが、DDSURFACEDESC へのポインターを含む構造体。 DirectX 6.0 以降では、これらのポインターが実際に DDSURFACEDESC2 構造体を指す、ポインターのまま LPDDSURFACEDESC として型指定された場合でも。 調べることができますが、ドライバーが選択した場合、 **dwSize**のメンバー、 [ **DDSURFACEDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff550339)ポインター、それによってポインターが実際を指すかどうかを決定し、 [ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)構造体。 ドライバーは、前 DirectX 6.0 のインストールで実行する必要があります、この確認を行うする必要があります。

返されるサイズが sizeof(DDSURFACEDESC2) の場合は、ドライバーが調べることができますし、 **dwCaps2**、 **dwCaps3**、および**dwCaps4**のメンバー、 [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)構造体。

 

 





