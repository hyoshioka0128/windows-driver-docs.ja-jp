---
title: ディスプレイ ドライバー (Windows 2000 モデル)
description: ディスプレイ ドライバー (Windows 2000 モデル)
ms.assetid: 9d49f4e7-5153-417e-8f15-42b3dcdf3fa6
keywords:
- ディスプレイドライバーモデル WDK Windows 2000、ドライバーの表示
- Windows 2000 display driver model WDK、display drivers
- ディスプレイドライバー WDK Windows 2000
- ディスプレイドライバー WDK Windows 2000、ディスプレイドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d59efe3b707c041299b3993503da4c04129083ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838991"
---
# <a name="display-drivers-windows-2000-model"></a>ディスプレイ ドライバー (Windows 2000 モデル)


## <span id="ddk_display_drivers_windows_2000_model__gg"></span><span id="DDK_DISPLAY_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


Microsoft NT ベースのオペレーティングシステム表示ドライバーライターは、次の2つの主要なソフトウェアインターフェイスに関係しています。

-   Graphics DDI インターフェイス-表示ドライバーが実装する関数のセット。 GDI はグラフィックスの DDI インターフェイスを呼び出して、グラフィックスコマンドを処理できます。

-   GDI インターフェイス--ドライバーの実装を簡素化するために、表示ドライバーによって呼び出されるシステム提供のヘルパールーチン。

ここでは、NT ベースのオペレーティングシステムの表示ドライバーおよびいくつかの実装情報に関連する主な概念について説明します。 プリンタードライバーとディスプレイドライバー (ドライバーの初期化と終了、グラフィックスの出力など) の両方に共通するグラフィックスドライバーの設計の[詳細については、「](using-the-graphics-ddi.md) GDI でのグラフィックス[ドライバーのサポート](gdi-support-for-graphics-drivers.md)」を参照してください。

ディスプレイドライバーライターは、次の DDIs を実装することもできます。

-   DirectDraw DDI--ベンダーが DirectDraw 用にハードウェアアクセラレータを提供できるようにするグラフィックスインターフェイス。 詳細については、「 [DirectDraw](directdraw.md) 」を参照してください。

-   Direct3D DDI--ベンダーが Direct3D 用にハードウェアアクセラレータを提供できるようにする3D グラフィックスインターフェイス。 詳細については、「 [DIRECT3D DDI](direct3d.md) 」を参照してください。

グラフィックス DDI エントリポイントと構造体、および GDI サービスの関数とオブジェクトの詳細については、「 [Gdi 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 





