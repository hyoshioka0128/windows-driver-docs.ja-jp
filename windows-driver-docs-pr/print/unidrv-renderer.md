---
title: Unidrv レンダラー
description: Unidrv レンダラー
ms.assetid: 5c19eb9c-149b-4587-a12d-f01164231b51
keywords:
- Unidrv、レンダラー
- WDK Unidrv レンダラー
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 757707092f723c9a93b3bd2b08a91bb5497510a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346522"
---
# <a name="unidrv-renderer"></a>Unidrv レンダラー





Unidrv レンダラーの実装として、[プリンター グラフィックス DLL](printer-graphics-dll.md)し、したがってグラフィック ドライバーの Microsoft デバイス ドライバー インターフェイス (DDI) で定義されている関数をエクスポートします。 アプリケーションでイメージをプリンター デバイスに送信するグラフィックス デバイス インターフェイス (GDI) 関数を呼び出すときに、カーネル モードのグラフィックス エンジンは DDI 関数レンダラーのグラフィックスを呼び出します。 これらのグラフィックス DDI 関数は、印刷ジョブのページのイメージの描画で GDI を支援します。

レンダラーは送信もプリンター コマンド シーケンス、スプーラーに印刷すると共に、イメージ データを表示するように指示、イメージとプリンターのハードウェアにコマンド。 レンダラーを送信するプリンターのコマンドがで指定された[Unidrv ミニドライバー](unidrv-minidrivers.md)します。

Unidrv のレンダリングの操作を変更するには、提供する、[プラグインでレンダリング](rendering-plug-ins.md)します。

 

 




