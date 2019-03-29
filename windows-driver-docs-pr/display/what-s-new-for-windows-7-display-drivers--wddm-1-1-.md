---
title: Windows 7 ディスプレイ ドライバー (WDDM 1.1) の新機能
description: Windows 7 ディスプレイ ドライバー (WDDM 1.1) の新機能
ms.assetid: 516A9C56-7ABC-49F4-8E92-3B6C3DB78CF6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d08fc2da06f6b9296128b24fc1c51afe7d9eec0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579476"
---
# <a name="whats-new-for-windows-7-display-drivers-wddm-11"></a>Windows 7 ディスプレイ ドライバー (WDDM 1.1) の新機能


Windows Driver Kit (WDK) にリリースされた Windows 7 では、ディスプレイ ドライバーのユーザー モードおよびカーネル モードの表示のミニポート ドライバーの新機能が含まれています。 Windows 7 と、新しい Microsoft Win32 Api は Windows 7 で使用できるデスクトップ ディスプレイの設定を制御する情報用に最適化されたディスプレイ ドライバーをインストールするための要件に更新プログラムも含まれています。

### <a name="span-idnewwindows7featuresforusermodedisplaydriversspanspan-idnewwindows7featuresforusermodedisplaydriversspannew-windows-7-features-for-user-mode-display-drivers"></a><span id="new_windows_7_features_for_user_mode_display_drivers"></span><span id="NEW_WINDOWS_7_FEATURES_FOR_USER_MODE_DISPLAY_DRIVERS"></span>ユーザー モードのディスプレイ ドライバーの Windows 7 の新機能

ユーザー モードのディスプレイ ドライバーの新しい Windows 7 の機能は次のとおりです。

[高解像度ビデオの処理](processing-high-definition-video.md)

[ビデオ コンテンツを保護します。](protecting-video-content.md)

[オーバーレイのサポートを確認しています](verifying-overlay-support.md)

[Direct3D のバージョン 11 をサポートしています。](supporting-direct3d-version-11.md)

[OpenGL のサポートの強化](supporting-opengl-enhancements.md)

[複数の GPU シナリオのリソースを管理します。](managing-resources-for-multiple-gpu-scenarios.md)

Windows 7 には、マイクロソフトの Direct3D バージョン 10.1 拡張形式対応も提供します。 拡張形式の認識の詳細については、次を参照してください。[拡張形式の認識をサポートしている](supporting-extended-format-awareness.md)します。

### <a name="span-idconnectingandconfiguringdisplaysspanspan-idconnectingandconfiguringdisplaysspanconnecting-and-configuring-displays"></a><span id="connecting_and_configuring_displays"></span><span id="CONNECTING_AND_CONFIGURING_DISPLAYS"></span>接続して表示の構成

デスクトップの表示の設定を制御する、新しい Win32 Api については、次を参照してください。[接続と構成が表示されます](connecting-and-configuring-displays.md)します。

### <a name="span-idnewwindows7featuresforkernelmodedisplayminiportdriversspanspan-idnewwindows7featuresforkernelmodedisplayminiportdriversspannew-windows-7-features-for-kernel-mode-display-miniport-drivers"></a><span id="new_windows_7_features_for_kernel_mode_display_miniport_drivers"></span><span id="NEW_WINDOWS_7_FEATURES_FOR_KERNEL_MODE_DISPLAY_MINIPORT_DRIVERS"></span>カーネル モードの表示のミニポート ドライバーを Windows 7 の新機能

Windows 7 で、次の機能を実行するには、カーネル モード ディスプレイ ミニポート ドライバーを開発することができます。

[接続と構成が表示されます - Ddi](ccd-ddis.md)

[GDI のハードウェア高速化](gdi-hardware-acceleration.md)

### <a name="span-idnewinfrequirementsspanspan-idnewinfrequirementsspannew-inf-requirements"></a><span id="new_inf_requirements"></span><span id="NEW_INF_REQUIREMENTS"></span>新しい INF 要件

Windows Vista のディスプレイ ドライバー モデルに書き込まれ、モデルの Windows 7 の機能用に最適化されたのディスプレイ ドライバーの INF ファイルには、複数の更新プログラムが必要です。 これらの更新プログラムについては、次を参照してください。[インストール ディスプレイ ドライバー最適化の Windows 7 以降](installing-display-drivers-optimized-for-windows-7-and-later.md)します。

### <a name="span-idgpuviewspanspan-idgpuviewspangpuview"></a><span id="gpuview"></span><span id="GPUVIEW"></span>GPUView

Windows 7 オペレーティング システムのリリースには、新しい開発ツール、グラフィックス処理装置 (GPU) のパフォーマンスを監視する GPUView (GPUView.exe) も導入されています。 GPUView の詳細については、次を参照してください。[を使用して GPUView](using-gpuview.md)します。

 

 





