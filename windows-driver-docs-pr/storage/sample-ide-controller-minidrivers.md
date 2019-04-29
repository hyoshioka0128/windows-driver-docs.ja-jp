---
title: サンプル IDE コントローラー ミニドライバー
description: サンプル IDE コントローラー ミニドライバー
ms.assetid: 3c8779ae-30d7-4ab8-b6d8-a711f917564c
keywords:
- IDE コント ローラー ミニドライバー WDK ストレージのサンプル
- 記憶域の IDE コント ローラー ミニドライバー WDK サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0133cceaa9056fa98cf0840d7e221bebbd98f715
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341256"
---
# <a name="sample-ide-controller-minidrivers"></a>サンプル IDE コントローラー ミニドライバー


## <span id="ddk_sample_ide_controller_minidrivers_kg"></span><span id="DDK_SAMPLE_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


このセクションでは、Microsoft Windows Driver Kit (WDK) に含まれているサンプルの IDE コント ローラー ミニドライバーを識別します。

WDK にはソース コードが含まれています、*問題は、pciide.sys*ミニドライバーの汎用コント ローラー。 サンプル コードを参照してください、 \\src\\WDK のストレージ ディレクトリ。

このサンプルは、64 ビット対応します。 Microsoft Visual C 6.0 を使用してビルドし、プラグ アンド プレイまたは電源の管理を実装しません。

*問題は、pciide.sys*サンプルは、Windows 95/98/Me、Windows 95/98/Me VxD 呼び出しが指定されていないオペレーティング システムの NT ベースのバージョン間のバイナリの互換性も、NT ベースのシステムの呼び出しは、ミニドライバーに埋め込まれます。

 

 




