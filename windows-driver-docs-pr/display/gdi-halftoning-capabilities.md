---
title: GDI ハーフトーン機能
description: GDI ハーフトーン機能
ms.assetid: 57274fd5-fdf6-4041-b52c-4e409465d159
keywords:
- レンダリング エンジンの GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、レンダリング エンジン
- 描画の WDK GDI レンダリング エンジン
- WDK GDI のレンダリング エンジン
- GDI WDK Windows 2000 の表示、ハーフトーン
- グラフィックス ドライバー WDK Windows 2000 の表示、ハーフトーン
- 描画の WDK GDI、ハーフトーン
- ハーフトーン WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 935fb1ac5cc4162e174ebf38c75706bd2fae111a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573585"
---
# <a name="gdi-halftoning-capabilities"></a>GDI ハーフトーン機能


## <span id="ddk_gdi_halftoning_capabilities_gg"></span><span id="DDK_GDI_HALFTONING_CAPABILITIES_GG"></span>


GDI ハーフトーン印刷デバイスや組み込みなどの機能がまだないディスプレイ デバイスの品質のディザーまたは色ハーフトーン イメージを生成します。 色のハーフトーンを提供します。

-   最高品質の色およびグレースケールの再現、特定のデバイスに対して実行できます。

-   限られた一連の輝度レベルのビジュアルの解像度を向上します。

-   別の出力デバイス間の相関関係を強化された色。

従来のアナログ ハーフトーンとは、ハーフトーン画面を使用する携帯電話のプロセスです。 ハーフトーン画面は、固定セル間のスペースを中心に、等しいサイズのセルで構成されます。 セルが固定の間隔では、各セル内のドットのサイズは継続的なトーンの印象を生成するために異なる場合に、インクの太さが対応します。

コンピューターでは、ほとんどの印刷や画面の網かけは固定のセルのピクセル サイズも使用します。 変数のドットのサイズをシミュレートするには、クラスターのピクセルの組み合わせは、ハーフトーン画面をシミュレートします。 Windows NT ベースのオペレーティング システムでは、GDI には、十分な最初の概算を提供するハーフトーン既定のパラメーターが含まれています。 その他のデバイスに固有の情報は、出力を向上させるために、システムに追加できます。

 

 





