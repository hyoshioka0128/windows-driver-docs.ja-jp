---
title: ディスプレイの色の管理
description: ディスプレイの色の管理
ms.assetid: a0c3f35f-3741-4d5a-b7ae-dd177c719508
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、色の管理
- Windows 2000 の WDK の色の管理を表示します。
- 画像の色の管理の WDK Windows 2000 の表示
- ICM WDK Windows 2000 の表示
- ガンマ ランプ WDK Windows 2000 を表示します。
- 色精度 WDK Windows 2000 の表示
- Windows 2000 の WDK の正確な色を表示します。
- WDK の Windows 2000 を調整する色を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a9395da8b7007a77225667c99b8d9dbfbd5aa53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354224"
---
# <a name="color-management-for-displays"></a>ディスプレイの色の管理


## <span id="ddk_color_management_for_displays_gg"></span><span id="DDK_COLOR_MANAGEMENT_FOR_DISPLAYS_GG"></span>


GDI は、イメージの色の管理 (ICM) バージョン 2.0 をサポートします。 ディスプレイ ドライバーは、特別なコードを実装することがなく ICM を使用できます。

ディスプレイ ハードウェアがサポートしている場合、*ガンマ ランプ*、ディスプレイ ドライバーを実装する必要があります[ **DrvIcmSetDeviceGammaRamp**](https://msdn.microsoft.com/library/windows/hardware/ff556243)します。 色の調整を色の精度を必要とするアプリケーションでは、この機能を使用します。 DirectDraw は、DirectX アプリケーション--RGB モードのパレットのアニメーションを実行するゲームなどを許可する - ガンマごとの傾斜増加を制御するためにもこの関数を使用します。 コード例を参照してください、 *Permedia*ディスプレイ ドライバーのサンプルです。

**注**   3 dlabs permedia2 チップが、Microsoft Windows Driver Kit (WDK) に含まれていない (*3dlabs.htm*) と 3 dlabs Permedia3 (*Perm3.htm*) ディスプレイ ドライバーのサンプルです。 これらのサンプル ドライバーから、Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロード可能を取得できます。

 

 

 





