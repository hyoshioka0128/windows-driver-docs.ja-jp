---
title: 最適化テクスチャ API
description: 最適化テクスチャ API
ms.assetid: 58d42807-3f52-415e-a06a-2ed408c20fb0
keywords:
- テクスチャ管理 WDK Direct3D、最適化されたテクスチャ
- 最適化されたテクスチャ WDK Direct3D
- CAPS2_HINTDYNAMIC
- DDSCAPS2_HINTSTATIC
- DDSCAPS2_OPAQUE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f704390e71e4d13bc0d7c3fb72c7aca4b2d52cb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379850"
---
# <a name="optimized-texture-api"></a>最適化テクスチャ API


## <span id="ddk_optimized_texture_api_gg"></span><span id="DDK_OPTIMIZED_TEXTURE_API_GG"></span>


次の 3 つの新しい機能では、DirectDrawSurface オブジェクトに適用できる、最適化のレベルを示します。 これらの caps ビットでは、DirectX 6.0 以降で、テクスチャのみをマークすることができます。 最適化された画面パラダイムは、セマンティクスできない可能性がありますのテクスチャの場合と同様ですが、サーフェスの他の種類をカバーする、将来拡張可能性があります。

これらの問題に対処する 3 つの新しいフラグがで提供される、 **DirectDrawSurface7:。作成**メソッド。 場合は、これら 3 つのフラグのいずれも指定、意思決定に修正プログラムまたはスィズル ドライバーに任されます。 これらのフラグは次のとおりです。

<span id="DDSCAPS2_HINTDYNAMIC"></span><span id="ddscaps2_hintdynamic"></span>DDSCAPS2\_HINTDYNAMIC  
ドライバーにストリーミング ビデオまたは手続き型テクスチャなどの用途のため、多くの場合、(たとえば、フレームごとに 1 回) にこの画面がロックされていることを示します。 このキャップを使用して解決*すべて*ドライバー列挙のテクスチャ サーフェスの形式。 ドライバーは、いくつかのオーバーヘッドが必要な場合に特に、これらのテクスチャのすべての変換を避ける必要があります。

<span id="DDSCAPS2_HINTSTATIC"></span><span id="ddscaps2_hintstatic"></span>DDSCAPS2\_HINTSTATIC  
これは、画面は、並べ替え/retiled/スィズルでドライバーを示します、 **IDirect3DDevice7::Load**と**IDirectDrawSurface7::Blt** (DirectDraw、Direct3D SDK で説明したメソッドSDK のドキュメントについては、それぞれ)。 この操作では、テクスチャのサイズは変更されません。 (ただし、そのときにパフォーマンスがかかります)、アプリケーションはこれらのビットをロックも可能性がありますので、比較的高速と対称でが。 ドライバーは、これらのサーフェスでロックに失敗することはできず、そのため、非可逆圧縮手法を使用することはできません。 ここで、MIP マップのサーフェスをインタリーブできます。

この上限は、いかなる場合においても、特にの特典が発生するパフォーマンスのスウィズ リングを強制的のものではありません。 いくつかのテクセル形式スィズルをサイレント モードで失敗します。

<span id="DDSCAPS2_OPAQUE"></span><span id="ddscaps2_opaque"></span>DDSCAPS2\_不透明  
これを示します、ドライバーにことによって、アプリケーションをもう一度このサーフェスはアクセスできません。 このフラグは、DDSCAPS2 ように動作\_HINTSTATIC フラグが実際の圧縮を許可する追加ハードウェア固有の圧縮スキームを使用します。 この操作が比較的低速には、対称のシンプルな圧縮スキームを許可する必要があります (など YUV 4:2:0、または色のセルの圧縮) を使用する 2 から 6 x への圧縮比率を提供します。 VQ などの非対称スキーム使わないでここで許容できないベンチマークしまうためです。

ドライバーでは、MIP マップ テクスチャを任意にインタリーブできます。 この手法とよいでしょう。 テクスチャがディスクから読み込まれるタイミングなどの内部レンダリング ループの外側にのみ要求されます。 このようなテクスチャが読み込まれた後のヒープ サイズのレポートは、圧縮が適用されている場合より少ないメモリ消費量を反映します。 テクスチャに追加のヘッダーのオーバーヘッドが、したがって多くの小さいテクスチャの圧縮は予想されるな量のメモリは保存されません。

一般に、テクスチャの圧縮率、またはこのフラグが含まれる圧縮品質に関する保証はありません。

次の場合にこのフラグを作成する画面が失敗します。

呼び出し、 **IDirectDrawSurface7::Lock**メソッド。

呼び出し、 **IDirectDrawSurface7::GetDC**メソッド。

このような表面に矩形を転送します。

このような画面からすべての転送。

このような画面にデータを格納する唯一の方法は、 **IDirect3DDevice7::Load**メソッド (Direct3D SDK のドキュメントで説明)、または完全な表面 blt 呼び出し。 詳細については**IDirectDrawSurface7::Lock**と**IDirectDrawSurface7::GetDC**、DirectDraw SDK ドキュメントを参照してください。

 

 





