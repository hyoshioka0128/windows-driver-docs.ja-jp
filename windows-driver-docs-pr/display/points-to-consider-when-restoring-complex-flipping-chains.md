---
title: 複合反転チェーンを復元する際の考慮点
description: 複合反転チェーンを復元する際の考慮点
ms.assetid: f368576f-a0a0-4def-888d-abf4fea8f6fb
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- チェーン WDK Direct3D の反転
- Z バッファー WDK Direct3D
- 反転チェーン WDK Direct3D を復元します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96d45245fe6cb0f83c1cc8b0cd7fb4d8b50c456
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383955"
---
# <a name="points-to-consider-when-restoring-complex-flipping-chains"></a>複合反転チェーンを復元する際の考慮点


## <span id="ddk_points_to_consider_when_restoring_complex_flipping_chains_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_RESTORING_COMPLEX_FLIPPING_CHAINS_GG"></span>


複雑なプライマリ画面が作成されると、可能性がありますか、接続されている Z バッファーをいない可能性があります。 サーフェスが復元されると、アプリケーションが Z バッファーの添付ファイルを追加することは。 ドライバー作成者注意すべきさまざまなシナリオで surface の添付ファイルのリストを使用すること[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)します。

表示される、一般的な手法、 *Perm3*ドライバーのサンプルを画面のマークを付けます**dwReserved1**場合フィールド*D3dCreateSurfaceEx*サーフェスが呼び出されます。 マークする場合に、だけドライバー **fpVidMem** (のメンバー、 [ **DD\_画面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造) が 0 と等しくないです。 これは、ため**fpVidMem**アプリケーションが、バック バッファーを明示的に接続されている Z バッファーに含まれていたプライマリ画面を復元するが、Z バッファーが復元されていないため、0 にする可能性があります。 後で Z バッファーをアプリケーションが復元され、ドライバー、マークされます。 プライマリのチェーンでは、ドライバーを復元する前に Z バッファーが、Z バッファーを既にマークされると、表示されるアプリケーションの復元がバックエンドに接続されている場合場合にバッファー *D3dCreateSurfaceEx*が呼び出されます。

> [!NOTE]
> Microsoft Windows Driver Kit (WDK) に 3 dlabs Permedia3 サンプルのディスプレイ ドライバーが含まれていません (*Perm3.h*)。 Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロードできるこのサンプル ドライバーを取得できます。

 

 

 





