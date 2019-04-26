---
title: 拡張サーフェス機能
description: 拡張サーフェス機能
ms.assetid: daa1a310-1cea-48ca-a373-a496b997424f
keywords:
- 描画サーフェイス機能 WDK の DirectDraw surface の拡張機能の詳細についてを拡張します。
- DirectDraw 拡張サーフェイス機能拡張セキュリティ機能についての WDK Windows 2000 の表示
- サーフェイス機能 WDK の DirectDraw surface の拡張機能の詳細についての拡張
- サーフェスの WDK DirectDraw、拡張機能
- 描画サーフェイス機能 WDK DirectDraw を拡張します。
- Windows 2000 の WDK 表示サーフェイスの機能を拡張し DirectDraw
- WDK DirectDraw surface の機能を拡張
- DDSCAPS2
- DD_MORESURFACECAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7a1fafc74e381b65f454c1676d087c86178860
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353364"
---
# <a name="extended-surface-capabilities"></a>拡張サーフェス機能


## <span id="ddk_extended_surface_capabilities_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


Microsoft DirectX 6.0 以降では、Microsoft DirectDraw には、以前のバージョンで見つかったもの以外のサーフェイスの機能が含まれています。 具体的にはいくつかの新しい構造体の追加を必要とこれらの機能を拡張、 [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)と[ **DD\_MORESURFACECAPS**](https://msdn.microsoft.com/library/windows/hardware/ff551659)構造体。 DDSCAPS2 構造に含まれる、 **dwCaps**メンバーが最初にある、 [ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)構造体が、次の 3 つの新しいメンバーも含まれます: **dwCaps2**、 **dwCaps3**、および**dwCaps4**します。 のみ**dwCaps2** DirectX 6.0 の DirectDraw に使用されます。 最後の 3 つのメンバー、 **DDSCAPS2** DDSCAPSEX 構造体の構造が配置されても同じです。

 

 





