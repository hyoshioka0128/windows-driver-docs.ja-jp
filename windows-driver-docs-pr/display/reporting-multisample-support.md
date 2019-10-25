---
title: マルチサンプル サポートのレポート
description: マルチサンプル サポートのレポート
ms.assetid: 05db3a79-08b3-4476-a016-d9a9bfa48504
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 の表示、マルチサンプリングレンダリング、レポート
- マルチサンプリングレンダリング WDK DirectX 8.0、レポート
- multisamples のレンダリング WDK DirectX 8.0、レポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a5ea2acaf081250355dfe8cfdc0e5936be3eb67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825935"
---
# <a name="reporting-multisample-support"></a>マルチサンプル サポートのレポート


## <span id="ddk_reporting_multisample_support_gg"></span><span id="DDK_REPORTING_MULTISAMPLE_SUPPORT_GG"></span>


ドライバーは、報告する各サーフェイス形式の1ピクセルあたりのサンプル数を指定することによって、関連付けられているハードウェアのマルチサンプリング機能を報告します。 [**Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の構造体が拡張され、 **MultiSampleCaps**という構造体が含まれるようになりました。 この構造体には、フリップ (全画面表示) と blt (ウィンドウ形式) のマルチサンプリングの両方について、ドライバーがピクセルあたりのサンプル数を表現できるようにするメンバーが含まれています。 これらの各メンバーは単語の種類であり、単語の値の各ビットは、1ピクセルあたりのサンプル数のサポートを示します。 このため、ドライバーは、1つの surface 形式のエントリを使用して、いくつかの異なるサンプル数のサポートを表現できます。

 

 





