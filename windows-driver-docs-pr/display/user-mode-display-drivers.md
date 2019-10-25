---
title: ユーザー モード ディスプレイ ドライバー
description: ユーザー モード ディスプレイ ドライバー
ms.assetid: cb4e8fb9-a2f0-43b2-ae9e-ccffa850ccd7
keywords:
- ディスプレイドライバーモデル WDK Windows Vista、ユーザーモード表示ドライバー
- Windows Vista display driver model WDK、ユーザーモード表示ドライバー
- ユーザーモード表示ドライバー WDK Windows Vista、ユーザーモード表示ドライバーについて
- ユーザーモード表示ドライバー WDK Windows Vista
- Direct3D WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a302a8dda67e3fb2e9174ee5aed066389baa493
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829296"
---
# <a name="user-mode-display-drivers"></a>ユーザー モード ディスプレイ ドライバー


## <span id="ddk_user_mode_display_drivers_gg"></span><span id="DDK_USER_MODE_DISPLAY_DRIVERS_GG"></span>


グラフィックスハードウェアベンダーは、ディスプレイアダプター用のユーザーモードの表示ドライバーを作成する必要があります。 ユーザーモードの表示ドライバーは、Microsoft Direct3D ランタイムによって読み込まれるダイナミックリンクライブラリ (DLL) です。 ユーザーモードの表示ドライバーは、少なくとも[Direct3D バージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)をサポートしている必要があります。 ユーザーモードの表示ドライバーでは、 [Direct3D バージョン 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)もサポートされています。 ユーザーモード表示ドライバーは、Direct3D version 9 DDI と Direct3D version 10 DDI の両方をサポートする1つの DLL で構成できます。また、2つの異なる Dll (バージョン9用と Direct3D DDI のバージョン10用) で構成することもできます。 次のトピックでは、ユーザーモードの表示ドライバーのさまざまな側面について説明します。

[ランタイム関数から受け取ったエラーコードを返す](returning-error-codes-received-from-runtime-functions.md)

[E\_INVALIDARG の戻り値の処理](handling-the-e-invalidarg-return-value.md)

[シェーダーコードの処理](processing-shader-codes.md)

[Direct3D の固定関数の状態の変換](converting-the-direct3d-fixed-function-state.md)

[深度ステンシルの値をコピーしています](copying-depth-stencil-values.md)

[インデックス値の検証](validating-index-values.md)

[複数のプロセッサのサポート](supporting-multiple-processors.md)

[複数のロックの処理](handling-multiple-locks.md)

[DirectX ビデオアクセラレーション2.0](directx-video-acceleration-2-0.md)

[サポート (Direct3D バージョン10を)](supporting-direct3d-version-10.md)

[サポート (Direct3D バージョン10.1 を)](supporting-direct3d-version-10-1.md)

[サポート (Direct3D バージョン11を)](supporting-direct3d-version-11.md)

[高解像度ビデオの処理](processing-high-definition-video.md)

[ビデオコンテンツの保護](protecting-video-content.md)

[オーバーレイサポートの確認](verifying-overlay-support.md)

[OpenGL の拡張機能のサポート](supporting-opengl-enhancements.md)

[複数の GPU シナリオ用のリソースの管理](managing-resources-for-multiple-gpu-scenarios.md)

 

 





