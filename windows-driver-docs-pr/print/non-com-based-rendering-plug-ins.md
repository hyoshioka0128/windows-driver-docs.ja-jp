---
title: 非 COM ベースのレンダリング プラグイン
description: 非 COM ベースのレンダリング プラグイン
ms.assetid: 435f9754-50be-4a4b-a5b4-b2bc8d66f034
keywords:
- レンダリングの COM ベースのプラグインを WDK の印刷
- COM ベースのレンダリング プラグイン WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8f0c019f5ea6951d76a0c6f8c55b7344aab901
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716981"
---
# <a name="non-com-based-rendering-plug-ins"></a>非 COM ベースのレンダリング プラグイン





プリンター ミニドライバーは、実装することでその機能の中核となるドライバーを通知、 [ **OEMEnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nf-printoem-oemenabledriver)のメンバーを設定する関数を[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)構造体。 **Pdrvfn**の配列のアドレスを持つこの構造体のメンバーを設定する必要があります[ **DRVFN** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_drvfn)構造体。 関数インデックスでは、およびアドレスのいずれかのこの配列の各要素を初期化する必要があります、 **OEM**_Xxx_それぞれ IHV が実装する関数。 (それぞれの詳細については、 **OEM**_Xxx_関数を参照してください[DDI フックの非 COM ベースの機能を](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index))。

アプリケーションがさらに、Win32 の GDI レンダリング タスクを実行する Microsoft Win32 GDI を呼び出すときに、通常のタスクを処理 Unidrv または Pscript5 コア ドライバーを呼び出します。 ただし、プリンターのミニドライバーが、特定の表示操作をフックすることは、コア ドライバーはプラグインのレンダリングの IHV にレンダリング タスクを渡すことに示されるかどうか。

たとえば、Win32 への呼び出しを作成するアプリケーションを**LineTo** API (Windows SDK のドキュメントで説明)。 一般に、この結果として別の呼び出しを中核となるドライバーの[ **DrvLineTo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto) DDI 線を描画します。 プリンター ミニドライバーに予定ただし、この DDI への呼び出しをフックすることが示される場合**DrvLineTo** IHV への呼び出しをすぐに転送[ **OEMLineTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nf-printoem-oemlineto)関数。

IHV を実装できます**OEMLineTo**で説明されているその他のアウト用のフック関数のいずれかまたは[DDI フックの非 COM ベースの機能を](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)されるため、レンダリング処理を完全に処理できるか、戻るで呼び出すことができますコアには、ドライバーは、その操作を処理します。

**OEMLineTo**の擬似コード例を次に示すように実装できます。

```cpp
BOOL APIENTRY
  OEMLineTo(
    SURFOBJ  *pso,
    CLIPOBJ  *pco,
    BRUSHOBJ  *pbo,
    LONG  x1,
    LONG  y1,
    LONG  x2,
    LONG  y2,
    RECTL  *prclBounds,
    MIX  mix
)
{
if ( OEM intends to handle the call ) {
 code to handle the call
}
else
// OEM calls Unidrv's DrvLineTo DDI
  bRetVal = (((PFN_DrvLineTo)(poempdev->pfnUnidrv[UD_DrvLineTo])) (
 pso,
            pco,
            pbo,
            x1,
            x2,
 y1,
            y2,
            prclBounds,
            mix,));
}
```

前の例では、式

```cpp
poempdev->pfnUnidrv[UD_DrvLineTo]
```

中核となるドライバーのアドレスに評価される**DrvLineTo** DDI します。 (**PFN\_DrvLineTo**) 前にある式は、適切な型への関数ポインターをキャストします。 各ここで示したアウト用のフック関数は、独自の関数ポインターに関連付けられます。

場合、 **OEM**_Xxx_ Unidrv core ドライバーと、画面に戻ります DDI 呼び出しデバイス管理の画面は、関連する、返すことによって、呼び出しを単純に無視できます Unidrv **FALSE**.

 

 




