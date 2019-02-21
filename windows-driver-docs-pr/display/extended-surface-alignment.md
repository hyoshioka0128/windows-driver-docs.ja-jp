---
title: 画面の配置の拡張
description: 画面の配置の拡張
ms.assetid: 3a91a826-7f57-4cad-b236-b41178ac3b17
keywords:
- 描画サーフェスの整列 WDK DirectDraw を拡張します。
- DirectDraw surface 配置 WDK Windows 2000 の表示を拡張します。
- サーフェスの WDK DirectDraw、配置の拡張
- WDK DirectDraw surface の配置の拡張
- ヒープ WDK DirectDraw
- 配置の WDK DirectDraw 拡張画面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7517b9a9019df36de76dd60474d2a58705963c8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550354"
---
# <a name="extended-surface-alignment"></a>画面の配置の拡張


## <span id="ddk_extended_surface_alignment_gg"></span><span id="DDK_EXTENDED_SURFACE_ALIGNMENT_GG"></span>


Microsoft DirectDraw では、ヒープあたりごとに画面のアラインメント要件をサポートしています。 このサポートは、Microsoft DirectX 5.0 で導入されました。 ドライバーは、四角形のヒープの X と Y の位置揃えを指定できますとピッチおよび線形のヒープの開始オフセットの位置揃え。 これらの配置では、さまざまな画面の種類は異なります。

いくつかのディスプレイ ハードウェアは、分割不可能な操作での表示の開始オフセットを設定することはできません。 表示期間の先頭には、このようなハードウェア ドライバーが途中で、値の設定でのみ、新しい開始、表示のオフセットをラッチのことができます。 DirectDraw には、ドライバーが表示されているバック バッファーのアラインメント要件を指定できるようになりました。 一部のハードウェアを 1 つだけのレジスタの書き込みを必要とする値の表示の開始オフセットを強制する可能性のある表示のバック バッファーのアラインメント要件を表現することができます。 この手法は、高頻度で、プライマリの画面が反転されるときに表示されないように不定期のちらつきを回避するのに役立ちます。

 

 





