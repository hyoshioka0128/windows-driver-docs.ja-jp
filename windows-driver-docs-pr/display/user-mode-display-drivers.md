---
title: ユーザー モード ディスプレイ ドライバー
description: ユーザー モード ディスプレイ ドライバー
ms.assetid: cb4e8fb9-a2f0-43b2-ae9e-ccffa850ccd7
keywords:
- ドライバー モデル WDK Windows Vista では、ユーザー モードのディスプレイ ドライバーの表示します。
- Windows Vista のディスプレイ ドライバー モデル WDK、ディスプレイ ドライバーのユーザー モード
- ユーザー モード ドライバー WDK Windows Vista の表示、ユーザー モードの詳細については、ディスプレイ ドライバー
- ディスプレイ ドライバー WDK Windows Vista のユーザー モード
- Direct3D の WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00dd1da159a813e24e99989f98bf053d3d46e5c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358920"
---
# <a name="user-mode-display-drivers"></a>ユーザー モード ディスプレイ ドライバー


## <span id="ddk_user_mode_display_drivers_gg"></span><span id="DDK_USER_MODE_DISPLAY_DRIVERS_GG"></span>


グラフィックス ハードウェア ベンダーは、そのディスプレイ アダプターのユーザー モードのディスプレイ ドライバーを記述する必要があります。 ユーザー モードのディスプレイ ドライバーは、マイクロソフトの Direct3D ランタイムによって読み込まれるダイナミック リンク ライブラリ (DLL) です。 ユーザー モードのディスプレイ ドライバーをサポートする必要がありますには少なくとも、 [Direct3D のバージョン 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)します。 ユーザー モードのディスプレイ ドライバーがサポートしているのも、 [Direct3D のバージョン 10 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552909)します。 ユーザー モードのディスプレイ ドライバーは、Direct3D バージョン 9 DDI と Direct3D のバージョンの両方のバージョン 9 のいずれかとその他の Direct3D DDI 10 のバージョンの 2 つの独立した Dll で構成できます DDI 10 またはをサポートする 1 つの DLL で構成できます。 次のトピックでは、ユーザー モードのディスプレイ ドライバーのさまざまな側面について説明します。

[ランタイム関数から受信したエラー コードを返す](returning-error-codes-received-from-runtime-functions.md)

[E を処理\_INVALIDARG 戻り値](handling-the-e-invalidarg-return-value.md)

[シェーダー コードの処理](processing-shader-codes.md)

[Direct3D の固定機能の状態に変換します。](converting-the-direct3d-fixed-function-state.md)

[深度ステンシルの値のコピー](copying-depth-stencil-values.md)

[インデックス値の検証](validating-index-values.md)

[複数のプロセッサをサポートしています。](supporting-multiple-processors.md)

[複数のロックを処理します。](handling-multiple-locks.md)

[DirectX のビデオ アクセラレータ 2.0](directx-video-acceleration-2-0.md)

[Direct3D のバージョン 10 のサポート](supporting-direct3d-version-10.md)

[サポートの Direct3D バージョン 10.1](supporting-direct3d-version-10-1.md)

[Direct3D のバージョン 11 をサポートしています。](supporting-direct3d-version-11.md)

[高解像度ビデオの処理](processing-high-definition-video.md)

[ビデオ コンテンツを保護します。](protecting-video-content.md)

[オーバーレイのサポートを確認しています](verifying-overlay-support.md)

[OpenGL のサポートの強化](supporting-opengl-enhancements.md)

[複数の GPU シナリオのリソースを管理します。](managing-resources-for-multiple-gpu-scenarios.md)

 

 





