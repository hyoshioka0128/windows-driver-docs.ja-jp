---
title: デバイス管理サーフェスを処理する
description: デバイス管理サーフェスを処理する
ms.assetid: 4403165f-c528-450e-9c96-77a9ce0778aa
keywords:
- Unidrv、サーフェスのデバイス管理
- デバイス管理のサーフェス WDK Unidrv
- 画面は、WDK Unidrv をデバイスが管理
- WDK Unidrv をグラフィックス DDI のフック関数します。
- DrvTextOut
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e468a5c320960b7d9f5d19ef2694499514f30f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378608"
---
# <a name="handling-device-managed-surfaces"></a>デバイス管理サーフェスを処理する





Unidrv では、印刷ページのイメージをレンダリングする描画サーフェスの GDI 管理が使用されます。 すべてのイメージはビットマップとしてレンダリングされます。 ベクトルを描画する機能など、このシナリオで利用されることは機能を使用したデバイスのデバイス管理の描画サーフェイスのカスタマイズされたドライバーのサポートを行うことができます。 デバイス管理の画面をサポートするために、次を実装するプラグインのレンダリングを提供する必要があります。

-   Unidrv でサポートされている画像がすべて DDI 描画関数の関数をフックのセット。 次の関数をフックする必要があります。[**DrvAlphaBlend**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)
    [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)
    [**DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)
     [ **DrvDitherColor**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)
    [**DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath) 
     [ **DrvGradientFill**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)
    [**DrvLineTo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto) 
     [ **DrvPlgBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)
    [**DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)
    [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt) 
     [ **DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)
    [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath) 
     [ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)
    [**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout) 
     [ **DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)
-   [ **IPrintOemUni::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enabledriver) Unidrv グラフィックス DDI フック関数へのポインターを提供するために使用するメソッド。

-   [ **IPrintOemUni::DriverDMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-driverdms)メソッドで、デバイス管理の画面が使用される Unidrv を通知し、画面に定義されたフック関数のどちらを使用するを指定します。

フック関数は、デバイス管理の画面に描画するときにも、GDI への Eng プレフィックス付きのサポート サービスに戻る呼び出すことはできません。 ただし、一時的なビットマップ画面を作成してへの Eng プレフィックス付きの描画機能に表示されるハンドルを渡すできます (を参照してください[、印刷ジョブのレンダリング](rendering-a-print-job.md))。

[ **IPrintOemUni::DriverDMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-driverdms)メソッドが呼び出された各プラグインのレンダリングは各レンダリング サーフェイス (GDI 管理またはデバイス管理) の種類を指定することもできます、印刷ジョブが、表示しようとしていますジョブ。 指定する必要があります、画面の任意のユーザー インターフェイスで選択可能なオプションに基づいて、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)します。

### <a name="drawing-text-on-a-device-managed-surface"></a>デバイス管理の画面でテキストの描画

プラグインのレンダリングが Unidrv をフックする必要があります[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout) (すべての他のグラフィックス DDI 描画関数) と共に関数。 デバイス管理の画面のテキストを作成するには、次の 4 つの関数間の相互作用が含まれます。

-   Unidrv の[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)関数

-   プラグインのレンダリング[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)フック関数

-   Unidrv の[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)メソッド

-   プラグインのレンダリング[ **IPrintOemUni::TextOutAsBitmap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)メソッド

デバイス管理の画面でテキストを表示するために必要な手順は次のとおりです。

1.  GDI 呼び出し Unidrv の[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)関数。

2.  Unidrv を呼び出す、レンダリング プラグインの[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)関数をフックします。

3.  フック関数は、テキストのブラシ、回転、およびクリップ領域を指定するデバイスにコマンドを送信します。

4.  フック関数には、Unidrv の[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)メソッドを使用するテキストを出力するフォントをダウンロードします。 このメソッドは、クリッピングのグリフに基づくも処理します。

5.  場合[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout) (フォントが利用できないか、回転) ために、ダウンロード可能なフォントを使用できません、呼び出し、レンダリング プラグインの[ **IPrintOemUni::TextOutAsBitmap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)メソッドで、ビットマップとしてテキストを描画します。

6.  後[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)から制御が戻る、 [ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)下線を描画する必要があります関数をフックし、strike スルーがで指定された四角形に基づく、 **DrvTextOut**関数の*prclExtra* (サポートされている) 場合は、ベクターのコマンドを使用して、パラメーター。

 

 




