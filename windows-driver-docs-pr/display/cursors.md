---
title: カーソル
description: カーソル
ms.assetid: 8647b0fc-b93b-489d-b2c0-b5caf98e800b
keywords:
- Windows 2000 の WDK の表示、カーソルの DirectX 8.0 リリース ノートします。
- カーソル WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd954bca92be289bc114c7f96b89586e1717d368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370760"
---
# <a name="cursors"></a>カーソル


## <span id="ddk_cursors_gg"></span><span id="DDK_CURSORS_GG"></span>


DirectX 8.0 がプライマリの画面に API レベルで直接アクセスしなくても高更新頻度のカーソルをサポートするための API を追加します。 DirectDraw blt とそれがエミュレートされるか、または機能を許可する場合、DirectX 8.0 は、カーソルは標準の GDI カーソルです。 DirectX カーソル API をサポートするためには、ドライバーは、D3DCAPS8 で機能の情報を返すには。

**CursorCaps** D3DCURSORCAPS にフィールドを設定する必要があります\_MONO、D3DCURSORCAPS\_色、またはその両方をモノクロのサポートを示すハードウェア カーソルの色します。 **MaxCursorEdgeSize**フィールドは、最大の幅の最小値とハードウェアのカーソル (またはハードウェアのカーソルがサポートされていない場合は 0) の最大の高さを設定する必要があります。 カーソルの高さと幅の異なる最大サイズを表現することはできません。

 

 





