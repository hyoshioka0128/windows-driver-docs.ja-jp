---
title: WDK ビルド出力
description: 既定では、WDK は、既定のビルド出力ディレクトリを指定するのに中間ディレクトリの $ (intdir) マクロを使用します。
ms.assetid: CD083755-9C9C-458A-9115-E63336C413B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0756e08abee528387f0b870c5c511140960a1a98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358080"
---
# <a name="wdk-build-output"></a>WDK ビルド出力


既定では、WDK は、中間ディレクトリを使用して **$ (intdir)** マクロを既定のビルド出力ディレクトリを指定します。

WDK と中間ディレクトリを定義する **$\\$ (configurationname)\\**します。 **$ (Configurationname)** マクロでは、たとえば、x64、ターゲットのバージョンの Windows と構成の種類 (リリースまたはデバッグ) が含まれている\\Win8.1Release します。

この方法では、同じバイナリの他の Windows ターゲットの前回のビルドを失うことがなくさまざまな構成で並列を構築できます。 このアプローチは通常のみが含まれます (x64、Win32) プラットフォームと構成の種類 (リリースでは、デバッグ)、名前の Windows デスクトップ アプリケーションを構築する場合に使用する可能性のある中間ディレクトリ。

 

 





