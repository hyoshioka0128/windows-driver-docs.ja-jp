---
title: ディスプレイ ドライバー (Windows 2000 モデル)
description: ディスプレイ ドライバー (Windows 2000 モデル)
ms.assetid: 9d49f4e7-5153-417e-8f15-42b3dcdf3fa6
keywords:
- ドライバー モデル WDK Windows 2000 では、ディスプレイ ドライバーの表示します。
- Windows 2000 ドライバー モデル WDK を表示、ディスプレイ ドライバー
- ディスプレイ ドライバー WDK Windows 2000
- ディスプレイ ドライバー WDK Windows 2000 では、ディスプレイ ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22034feca55983d2f758d4ded33fa7aebb770a5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379366"
---
# <a name="display-drivers-windows-2000-model"></a>ディスプレイ ドライバー (Windows 2000 モデル)


## <span id="ddk_display_drivers_windows_2000_model__gg"></span><span id="DDK_DISPLAY_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


2 つのコア ソフトウェア インターフェイスでは Microsoft NT ベースのオペレーティング システムのディスプレイ ドライバー作成者です。

-   グラフィックス DDI インターフェイス--、ディスプレイ ドライバーを実装する関数のセットです。 GDI は、グラフィックス コマンドを処理するグラフィックス DDI インターフェイスを呼び出すことができます。

-   GDI インターフェイスによって呼び出されるシステム提供のヘルパー ルーチンは、ドライバーをドライバーの実装を簡略化を表示します。

このセクションでは、いくつか実装情報だけでなく、NT ベースのオペレーティング システムのディスプレイ ドライバーに関連付けられている主要な概念について説明します。 参照してください[グラフィック ドライバーのサポートを GDI](gdi-support-for-graphics-drivers.md)と[グラフィックス DDI を使用して](using-the-graphics-ddi.md)グラフィックス ドライバー設計の詳細は、両方のプリンター ドライバーに共通し、ドライバー、ドライバーの初期化などを表示するのと終了、およびグラフィックスの出力。

ディスプレイ ドライバー開発者は、次 Ddi も実装できます。

-   DirectDraw DDI--グラフィックス インターフェイスにより、DirectDraw のハードウェア アクセラレーションを提供するベンダーです。 参照してください[DirectDraw](directdraw.md)詳細についてはします。

-   Direct3D DDI--Direct3D のハードウェア アクセラレーションを提供するベンダーは、3 D グラフィックス インターフェイス。 参照してください[Direct3D DDI](direct3d.md)詳細についてはします。

グラフィックス DDI エントリ ポイントと構造体、および GDI サービス関数と、オブジェクト参照の詳細については[GDI 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 





