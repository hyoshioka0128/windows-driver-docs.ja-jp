---
title: 複数サンプル レンダリングの品質の管理
description: 複数サンプル レンダリングの品質の管理
ms.assetid: 5a2f2d36-ab0d-4267-a921-c42621fa5d47
keywords:
- 複数の標本 WDK DirectX 9.0 のレンダリング、品質を制御します。
- レンダリング multisamples WDK DirectX 9.0、品質を制御します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4b71247737f24c1e33a4bb1da921d907d3796e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370298"
---
# <a name="controlling-quality-of-multiple-sample-rendering"></a>複数サンプル レンダリングの品質の管理


## <span id="ddk_controlling_quality_of_multiple_sample_rendering_gg"></span><span id="DDK_CONTROLLING_QUALITY_OF_MULTIPLE_SAMPLE_RENDERING_GG"></span>


呼び出す必要がありますが、アプリケーションは、特定のサンプリング方法では、画面を作成する要求できます、前に、 **IDirect3D9::CheckDeviceMultiSampleType**ディスプレイ デバイスがその手法をサポートしているかを確認するメソッド。 さらに、ランタイムに送信、 **GetDriverInfo2**要求を使用して、 **D3DGDI2\_型\_GETMULTISAMPLEQUALITYLEVELS**の品質レベルの数を取得する値、特定のマルチ サンプリング種類と手法に関連付けられたサーフェスの書式。 詳細については**GetDriverInfo2**を参照してください[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

デバイスのドライバーの数を指定する必要があります、ディスプレイ デバイスは、マスクのマルチ サンプリング (複数の標本のレンダー ターゲット形式プラス アンチ エイリアスのサポートの 1 つ以上のサンプル) またはだけ nonmaskable マルチ サンプリング (アンチ エイリアスのみサポート) をサポートするかどうか品質レベル、D3DMULTISAMPLE\_マスク不可能複数サンプルの種類。 アンチエイリアシングのためだけのマルチ サンプリングを使用するアプリケーションは、ドライバーがサポートするマスク不可能複数サンプル品質レベルの数を照会するのみ必要ですし。

ディスプレイ デバイスがマルチ サンプリングの手法をサポートしているかどうかを確認するだけでなく**IDirect3D9::CheckDeviceMultiSampleType**も、この手法に関連付けられている品質レベルの数を返します。

アプリケーションは、サーフェスを作成する要求、サーフェスの形式、マルチ サンプリングの種類とそのサポートを以前に確認する品質レベルの数の組み合わせが使用されます。 これにより、画面が正常に作成します。 ランタイムが呼び出す、ドライバーの[ *DdCanCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))、 [ *DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))、または[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)サーフェスを作成する関数。 この呼び出しで、ランタイムは 5 ビットにマルチ サンプリングされたサーフェイスでのサンプルの数をエンコードします (、DDSCAPS3\_マルチ サンプリング\_マスク マスク) と複数サンプル品質レベルを 3 つのビット数 (、DDSCAPS3\_マルチ サンプリング\_品質\_マスク マスク) の**dwCaps3**のメンバー、 [ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))サーフェイスでの構造体。

詳細については**IDirect3D9::CheckDeviceMultiSampleType**、DirectX SDK の最新のドキュメントを参照してください。

 

 





