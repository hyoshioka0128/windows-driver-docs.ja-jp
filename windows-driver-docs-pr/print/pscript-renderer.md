---
title: Pscript レンダラー
description: Pscript レンダラー
ms.assetid: b1707a83-c5c9-4578-8603-7c19de4960ed
keywords:
- PostScript プリンター ドライバー WDK の印刷、レンダラー
- Pscript WDK の印刷、レンダラー
- WDK Pscript レンダラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee28253b9faab9a5bd14abaaacaa30a42b5c3fbc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554007"
---
# <a name="pscript-renderer"></a>Pscript レンダラー





Pscript レンダラーの実装として、[プリンター グラフィックス DLL](printer-graphics-dll.md)し、したがってグラフィック ドライバーの Microsoft デバイス ドライバー インターフェイス (DDI) で定義されている関数をエクスポートします。 アプリケーションは、テキストとイメージをプリンター デバイスに送信するグラフィックス デバイス インターフェイス (GDI) 関数を呼び出すときに、カーネル モードのグラフィックス エンジンは DDI 関数レンダラーのグラフィックスを呼び出します。 これらのグラフィックス DDI 関数は、印刷ジョブのページのイメージの描画で GDI を支援します。

レンダラー、印刷スプーラー、データ ストリームとプリンターのハードウェアにコマンドを送りますにテキストを描画イメージ データのプリンターとコマンドのシーケンスを送信するためも担当します。

Pscript のレンダリングの操作を変更するには、提供する、[プラグインでレンダリング](rendering-plug-ins.md)、というタイトルのセクションに記載されている[をカスタマイズする Microsoft のプリンター ドライバー](customizing-microsoft-s-printer-drivers.md)します。

 

 




