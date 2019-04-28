---
title: ドライバーの観点からの GDI
description: ドライバーの観点からの GDI
ms.assetid: 2a6769ea-c6ae-4397-a5e4-f38964d2d8d1
keywords:
- GDI WDK Windows 2000 の表示、ドライバーの通信
- グラフィックス ドライバー WDK Windows 2000 の表示、ドライバーの通信
- 描画 WDK GDI やドライバーの通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a8cde56bd38f37d2b3c1d91307d59adfe8bf267
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363813"
---
# <a name="gdi-from-the-drivers-perspective"></a>ドライバーの観点からの GDI


## <span id="ddk_gdi_from_the_driver_92_s_perspective_gg"></span><span id="DDK_GDI_FROM_THE_DRIVER_92_S_PERSPECTIVE_GG"></span>


GDI は、Microsoft Windows NT ベースのグラフィックス ドライバーとアプリケーションの間の中間のサポートです。 アプリケーションでは、グラフィック出力要求を行う Microsoft Win32 GDI 関数を呼び出します。 これらの要求は、カーネル モードの GDI にルーティングされます。 次に、カーネル モードの GDI は、ディスプレイ ドライバーやプリンター ドライバーなど、適切なグラフィック ドライバーをこれらの要求を送信します。 カーネル モードの GDI は、置き換えることのできないシステム提供のモジュールです。

GDI は、一連のグラフィックス デバイス ドライバー インターフェイス (DDI グラフィックス) 関数を使ってグラフィックス ドライバーと通信します。 これらの関数がで識別される、 *Drv*プレフィックス。 情報は、GDI とドライバーのこれらのエントリ ポイントの入力/出力パラメーターを介して渡されます。 ドライバー*する必要があります*サポート特定*DrvXxx* GDI を呼び出すための関数。 ドライバーは、GDI に戻る前に、関連するハードウェアで適切な操作を実行することによって、GDI の要求をサポートします。

GDI には、ドライバーがこれらの機能をサポートする必要がなくなります自体、およびそれに、ドライバーのサイズを小さくことによって多くのグラフィックス出力機能が含まれています。 GDI には、さらに、ドライバーが提供する必要がありますサポートの量を減らす、ドライバーが呼び出すことができるサービス機能もエクスポートします。 サービスの GDI 関数がで識別される、**への Eng**プレフィックス、および GDI で維持される構造体へのアクセスを提供する機能は、フォームの名前を持つ*Xxx*<strong>OBJ *\_</strong>* * Xxx*します。

次の図は、この通信の流れを示します。

![グラフィックス ドライバーとグラフィックス デバイス インターフェイス (gdi) の相互作用を示す図](images/gditoddi.png)

 

 





