---
title: 拡張の表面の配置を使用します。
description: 拡張の表面の配置を使用します。
ms.assetid: ae4a6820-b9be-4dd2-95d8-6030b3b63826
keywords:
- 描画サーフェスの整列 WDK DirectDraw を拡張します。
- DirectDraw surface 配置 WDK Windows 2000 の表示を拡張します。
- サーフェスの WDK DirectDraw、配置の拡張
- WDK DirectDraw surface の配置の拡張
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e68b780388d33aab5afb35918332b81ef8b7b160
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539661"
---
# <a name="using-extended-surface-alignment"></a>拡張の表面の配置を使用します。


## <span id="ddk_using_extended_surface_alignment_gg"></span><span id="DDK_USING_EXTENDED_SURFACE_ALIGNMENT_GG"></span>


サーフェス配置の拡張機能を有効にするには、DirectDraw ドライバーは、初期化時に次のタスクを実行する必要があります。

-   ドライバーを指定する必要があります、 [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)で機能、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627) DirectDraw できる構造体追加情報を取得する呼び出しです。

-   *DdGetDriverInfo*の GUID を持つコールバックが呼び出される\_GetHeapAlignment GUID を指定します。 ドライバーを入力する必要があります、 [ **DD\_GETHEAPALIGNMENTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551572)構造体、し、この構造のコピー、 **lpvData**のメンバー、 [ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)構造体。

ドライバーを入力する必要があります、 [ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)で示される構造体、 [ **HEAPALIGNMENT** ](https://msdn.microsoft.com/library/windows/hardware/ff567265)または、DDSCAPS の論理構造\_このヒープ内の配置が必要なサーフェスの種類にかかわらず xxxx フラグ。 DDSCAPS のビットを設定するとかどうか、は、適切な表現、配置制限商務 DirectDraw [ **SURFACEALIGNMENT** ](https://msdn.microsoft.com/library/windows/hardware/ff569895)構造体のメンバー。 DDSCAPS\_フリップ ビット、 **FlipTarget**メンバーでは、可能性のあるプライマリ (表示) 画面をプライマリ反転バッファー チェーンは、バックアップが画面に適用します。 現在許可されている一連の配置を指定できますサーフェスの機能を次に示します。

-   DDSCAPS\_OFFSCREENPLAIN

-   DDSCAPS\_EXECUTEBUFFER

-   DDSCAPS\_オーバーレイ

-   DDSCAPS\_テクスチャ

-   DDSCAPS\_ZBUFFER

-   DDSCAPS\_アルファ

-   DDSCAPS\_反転

**注**   DirectDraw 内のエントリと新しい画面の機能を比較し、 [ **HEAPALIGNMENT** ](https://msdn.microsoft.com/library/windows/hardware/ff567265)構造が指定されている順序で。 DDSCAPS で surface など\_MIPMAP |DDSCAPS\_テクスチャ |DDSCAPS\_に従ってフリップ セットを配置、**テクスチャ**、HEAPALIGNMENT のメンバーが構造体、ビット単位でアラインメントが指定された最初の適用可能な機能です (つまり、 **テクスチャの**前に表示された**FlipTarget** HEAPALIGNMENT 構造で)。 **FlipTarget**メンバーがこの例ではないと見なされます。 DDSCAPS プライマリ フリッピング チェーン内のバック バッファーが設定されているため\_に従ってこのような画面を固定反転は、アラインメントを指定できる他のビットなし、 **FlipTarget**メンバー。 プライマリのフリッピング チェーン (としてプライマリの画面サイズと同じピクセル形式を持つもの) のメンバーになる可能性のあるサーフェスがに従って配置も、 **FlipTarget**メンバー。

 

 

 





