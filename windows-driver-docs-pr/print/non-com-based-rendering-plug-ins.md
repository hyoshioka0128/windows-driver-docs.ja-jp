---
title: 非 COM ベースのレンダリング プラグイン
description: 非 COM ベースのレンダリング プラグイン
ms.assetid: 435f9754-50be-4a4b-a5b4-b2bc8d66f034
keywords:
- 非 COM ベースのレンダリングプラグイン WDK 印刷
- レンダリングプラグイン WDK print、非 COM ベース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edba3952df5128892839b25d378ee8429c0157c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837563"
---
# <a name="non-com-based-rendering-plug-ins"></a>非 COM ベースのレンダリング プラグイン





Printer ミニドライバーは、 [**Oemenabledriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nf-printoem-oemenabledriver)関数を実装することによって、その機能のコアドライバーに通知します。この関数は、 [**Dr abledata**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)構造体のメンバーを入力します。 この構造体の**pdrvfn**メンバーは、 [**DRVFN**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_drvfn)構造体の配列アドレスを使用して設定する必要があります。 この配列の各要素は、関数インデックスと、IHV が実装している**OEM**_Xxx_関数のいずれかのアドレスを使用して初期化する必要があります。 (各**OEM**_Xxx_関数の詳細な説明については、「[非 COM ベースの DDI フック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)」を参照してください)。

アプリケーションが Microsoft Win32 GDI を呼び出してレンダリングタスクを実行すると、Win32 GDI は、通常、タスクを処理する Unidrv または Pscript5 core ドライバーを呼び出します。 ただし、プリンターミニドライバーが特定のレンダリング操作をフックできることを示している場合、コアドライバーは、レンダリングタスクを IHV レンダリングプラグインに渡します。

たとえば、Win32 **LineTo** API (Windows SDK のドキュメントで説明) を呼び出すアプリケーションを考えてみます。 通常、このような場合は、コアドライバーの[**DrvLineTo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto) DDI を呼び出して、直線を描画します。 ただし、プリンタミニドライバーがこの DDI への呼び出しをフックするように指定している場合、 **DrvLineTo**は直ちに IHV の[**oemlineto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nf-printoem-oemlineto)関数への呼び出しを転送します。

IHV は、 **Oemlineto**を実装できます。または、[非 COM ベースの DDI フック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)に記述されている他のすべてのフック関数を実装して、レンダリング操作を完全に処理できるようにするか、コールバックしてコアドライバーがその操作を処理できるようにすることができます。

次の擬似コード例に示すように、 **Oemlineto**を実装できます。

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

コアドライバーの**DrvLineTo** DDI のアドレスに評価されます。 関数ポインターを適切な型にキャストする (**PFN\_DrvLineTo**) 式。 このセクションに記載されている各フック関数は、独自の関数ポインターに関連付けられています。

**OEM**_Xxx_ DDI が Unidrv コアドライバーにコールバックし、関連するサーフェイスがデバイスで管理されている場合、Unidrv は**FALSE**を返すことによって、単に呼び出しを無視することに注意してください。

 

 




