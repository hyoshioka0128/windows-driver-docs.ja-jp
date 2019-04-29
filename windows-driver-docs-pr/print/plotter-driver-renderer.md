---
title: プロッター ドライバー レンダラー
description: プロッター ドライバー レンダラー
ms.assetid: 54aac978-6344-41b3-97ea-e78816fb94dc
keywords:
- プロッター ドライバー WDK の印刷、レンダラー
- MSPlot WDK の印刷、レンダラー
- WDK MSPlot レンダラー
- グラフィックス DDI 関数 WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53553fab1f200eaab54c48e03da6c2b26e1cf324
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386617"
---
# <a name="plotter-driver-renderer"></a>プロッター ドライバー レンダラー





プロッター ドライバーのレンダラーとして実装されている、[プリンター グラフィックス DLL](printer-graphics-dll.md)し、したがってグラフィック ドライバーの Microsoft デバイス ドライバー インターフェイス (DDI) で定義されている関数をエクスポートします。 アプリケーションがプロッターにイメージを送信するグラフィックス デバイス インターフェイス (GDI) 関数を呼び出すときに、カーネル モードのグラフィックス エンジンは DDI 関数レンダラーのグラフィックスを呼び出します。 これらのグラフィックス DDI 関数は、印刷ジョブのページのイメージの描画で GDI を支援します。

レンダラーは送信もプロッター コマンド シーケンス、スプーラーに印刷すると共に、イメージ データを表示し、イメージと指示プロッターのハードウェアにコマンド。

 

 




