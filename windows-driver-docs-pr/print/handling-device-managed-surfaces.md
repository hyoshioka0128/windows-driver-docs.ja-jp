---
title: デバイス管理サーフェスを処理する
description: デバイス管理サーフェスを処理する
ms.assetid: 4403165f-c528-450e-9c96-77a9ce0778aa
keywords:
- Unidrv、デバイスで管理されたサーフェイス
- デバイスで管理されているサーフェス WDK Unidrv
- surface デバイスで管理されている WDK Unidrv
- グラフィックス DDI 関数のフック (WDK Unidrv)
- DrvTextOut
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b3f979ffe047efb92e335d582e4678b4ea8b67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843410"
---
# <a name="handling-device-managed-surfaces"></a>デバイス管理サーフェスを処理する





Unidrv が印刷ページイメージをレンダリングするときに、GDI が管理する描画サーフェイスを使用します。 すべての画像はビットマップとしてレンダリングされます。 ベクターを描画する機能など、このシナリオでは利用できない機能を持つデバイスの場合、デバイス管理の描画サーフェイスに対してドライバーのサポートをカスタマイズすることができます。 デバイスで管理されたサーフェイスをサポートするには、次のものを実装するレンダリングプラグインを用意する必要があります。

-   Unidrv でサポートされているすべてのグラフィックス DDI 描画関数のフック関数のセット。 次の関数をフックする必要があります: [**Drvalphablend**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)
    [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)
    [**DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)
    [**DrvDitherColor**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)
    [**DrvFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)
    [**DrvGradientFill**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)
    [**DrvLineTo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)
    [**DrvPlgBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)
    [**DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)
    [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)
    [**DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)
    [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)
    [**DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)
    [**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)
    [**DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)
-   [**Iprintoemuni:: EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)メソッド。グラフィックス DDI フック関数へのポインターを Unidrv に提供するために使用されます。

-   [**Iprintoemuni::D riverDMS メソッド。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms)これは、デバイスで管理されたサーフェイスが使用されることを Unidrv に通知し、定義されているフック関数のうち、どの部分をサーフェイスに使用するかを指定します。

デバイスで管理されたサーフェイスで描画する場合、フック関数は、GDI の Eng プレフィックス付きサポートサービスにコールバックすることはできません。 ただし、一時ビットマップサーフェイスを作成し、そのサーフェイスのハンドルを Eng で始まる描画関数に渡すことができます (「[印刷ジョブのレンダリング](rendering-a-print-job.md)」を参照してください)。

[**Iprintoemuni::D riverDMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms)メソッドは印刷ジョブがレンダリングされるたびに呼び出されるため、レンダリングプラグインでは、各ジョブのレンダリングサーフェイスの種類 (GDI 管理またはデバイス管理) を指定できます。 ユーザーインターフェイスで選択可能なオプションの面での選択に基づいて、[ユーザーインターフェイスプラグイン](user-interface-plug-ins.md)も提供する必要があります。

### <a name="drawing-text-on-a-device-managed-surface"></a>デバイスで管理された画面でのテキストの描画

レンダリングプラグインは、Unidrv の[**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)関数を、他のすべてのグラフィックス DDI 描画関数と共にフックする必要があります。 デバイスで管理されたサーフェイスのテキストを作成するには、次の4つの機能間の相互作用が必要です。

-   Unidrv の[**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)関数

-   プラグインの[**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)フック関数のレンダリング

-   Unidrv の[**Iprintoemdriveruni::D rvunitextout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)メソッド

-   レンダリングプラグインの[**Iprintoemuni:: TextOutAsBitmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)メソッド

デバイスで管理されたサーフェイスでのテキストの表示には、次の手順が含まれます。

1.  GDI は Unidrv の[**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)関数を呼び出します。

2.  Unidrv は、レンダリングプラグインの[**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)フック関数を呼び出します。

3.  フック関数は、テキストのブラシ、回転、およびクリップ領域を指定するために、デバイスにコマンドを送信します。

4.  フック関数は、Unidrv の[**Iprintoemdriveruni::D rvunitextout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)メソッドを呼び出します。このメソッドは、ダウンロードしたフォントを使用してテキストを出力します。 このメソッドは、グリフベースのクリッピングも処理します。

5.  [**Iprintoemdriveruni::D rvunitextout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)がダウンロード可能なフォントを使用できない場合 (フォントが使用できないか、回転されているため)、テキストをビットマップとして描画するレンダリングプラグインの[**Iprintoemuni:: TextOutAsBitmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)メソッドを呼び出します。

6.  [**Iprintoemdriveruni::D rvunitextout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)が返された後、 [**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)フック関数は、 **DrvTextOut**関数の*prclextra*パラメーターで指定された四角形に基づいて、次のように下線と打ち消し線を描画する必要があります。ベクターコマンド (サポートされている場合)。

 

 




