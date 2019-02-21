---
title: プロッター ドライバーのレンダラー
description: プロッター ドライバーのレンダラー
ms.assetid: 54aac978-6344-41b3-97ea-e78816fb94dc
keywords:
- プロッター ドライバー WDK の印刷、レンダラー
- MSPlot WDK の印刷、レンダラー
- WDK MSPlot レンダラー
- グラフィックス DDI 関数 WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53553fab1f200eaab54c48e03da6c2b26e1cf324
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550079"
---
# <a name="plotter-driver-renderer"></a>プロッター ドライバーのレンダラー





プロッター ドライバーのレンダラーとして実装されている、[プリンター グラフィックス DLL](printer-graphics-dll.md)し、したがってグラフィック ドライバーの Microsoft デバイス ドライバー インターフェイス (DDI) で定義されている関数をエクスポートします。 アプリケーションがプロッターにイメージを送信するグラフィックス デバイス インターフェイス (GDI) 関数を呼び出すときに、カーネル モードのグラフィックス エンジンは DDI 関数レンダラーのグラフィックスを呼び出します。 これらのグラフィックス DDI 関数は、印刷ジョブのページのイメージの描画で GDI を支援します。

レンダラーは送信もプロッター コマンド シーケンス、スプーラーに印刷すると共に、イメージ データを表示し、イメージと指示プロッターのハードウェアにコマンド。

 

 




