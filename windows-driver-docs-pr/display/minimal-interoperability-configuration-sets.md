---
title: 最小限の相互運用性構成セット
description: 最小限の相互運用性構成セット
ms.assetid: 2390c710-8693-4af4-903f-89068436141d
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、制限付きのプロファイル
- ビデオ アクセラレータ WDK DirectX、制限付きのプロファイル
- VA WDK DirectX、制限付きのプロファイル
- 制限付きプロファイル WDK DirectX VA
- 最小限の相互運用性の構成設定の WDK DirectX VA
- 相互運用性の構成設定の WDK DirectX VA
- WDK DirectX VA を設定します。
- DXVA_ConfigPictureDecode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac5c3548e2f3930f3dcc1f7b5cb323fe6c46a6fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385033"
---
# <a name="minimal-interoperability-configuration-sets"></a>最小限の相互運用性構成セット


## <span id="ddk_minimal_interoperability_configuration_sets_gg"></span><span id="DDK_MINIMAL_INTEROPERABILITY_CONFIGURATION_SETS_GG"></span>


すべての DirectX VA デコーダーが使用するすべての DirectX VA アクセラレータで動作する必要があります、[制限プロファイル](restricted-profiles.md)します。 すべてデコーダーは、メンバー、一連の接続の構成と操作の対応である必要があり、各アクセラレータ キーは、そのセットの少なくとも 1 つのメンバーと操作の対応である必要があります。 これには、デバイス ドライバーが提供する必要があります機能の最小レベルを定義する 3 つの構成セットがあります。

[圧縮する画像のセットをデコード](compressed-picture-decoding-set.md)

[アルファ ブレンドのデータのセットの読み込み](alpha-blend-data-loading-set.md)

[アルファ ブレンドの組み合わせのセット](alpha-blend-combination-set.md)

それぞれのデコーダーを設定し、アクセラレータは同じ DirectX VA モードが制限されている GUID をサポートする必要があります。

 

 





