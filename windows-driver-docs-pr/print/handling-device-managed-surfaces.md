---
title: デバイス管理のサーフェスの処理
description: デバイス管理のサーフェスの処理
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
ms.openlocfilehash: 11ef3cdd7232649b0c3f5ad1a70e77c471db6ed2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537435"
---
# <a name="handling-device-managed-surfaces"></a>デバイス管理のサーフェスの処理





Unidrv では、印刷ページのイメージをレンダリングする描画サーフェスの GDI 管理が使用されます。 すべてのイメージはビットマップとしてレンダリングされます。 ベクトルを描画する機能など、このシナリオで利用されることは機能を使用したデバイスのデバイス管理の描画サーフェイスのカスタマイズされたドライバーのサポートを行うことができます。 デバイス管理の画面をサポートするために、次を実装するプラグインのレンダリングを提供する必要があります。

-   Unidrv でサポートされている画像がすべて DDI 描画関数の関数をフックのセット。 次の関数をフックする必要があります。[**DrvAlphaBlend**](https://msdn.microsoft.com/library/windows/hardware/ff556176)
    [**DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)
    [**DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)
     [ **DrvDitherColor**](https://msdn.microsoft.com/library/windows/hardware/ff556202)
    [**DrvFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556220) 
     [ **DrvGradientFill**](https://msdn.microsoft.com/library/windows/hardware/ff556236)
    [**DrvLineTo** ](https://msdn.microsoft.com/library/windows/hardware/ff556245) 
     [ **DrvPlgBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556258)
    [**DrvRealizeBrush**](https://msdn.microsoft.com/library/windows/hardware/ff556273)
    [**DrvStretchBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556302) 
     [ **DrvStretchBltROP**](https://msdn.microsoft.com/library/windows/hardware/ff556306)
    [**DrvStrokeAndFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556311) 
     [ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)
    [**DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277) 
     [ **DrvTransparentBlt**](https://msdn.microsoft.com/library/windows/hardware/ff557283)
-   [ **IPrintOemUni::EnableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff554248) Unidrv グラフィックス DDI フック関数へのポインターを提供するために使用するメソッド。

-   [ **IPrintOemUni::DriverDMS** ](https://msdn.microsoft.com/library/windows/hardware/ff554245)メソッドで、デバイス管理の画面が使用される Unidrv を通知し、画面に定義されたフック関数のどちらを使用するを指定します。

フック関数は、デバイス管理の画面に描画するときにも、GDI への Eng プレフィックス付きのサポート サービスに戻る呼び出すことはできません。 ただし、一時的なビットマップ画面を作成してへの Eng プレフィックス付きの描画機能に表示されるハンドルを渡すできます (を参照してください[、印刷ジョブのレンダリング](rendering-a-print-job.md))。

[ **IPrintOemUni::DriverDMS** ](https://msdn.microsoft.com/library/windows/hardware/ff554245)メソッドが呼び出された各プラグインのレンダリングは各レンダリング サーフェイス (GDI 管理またはデバイス管理) の種類を指定することもできます、印刷ジョブが、表示しようとしていますジョブ。 指定する必要があります、画面の任意のユーザー インターフェイスで選択可能なオプションに基づいて、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)します。

### <a name="drawing-text-on-a-device-managed-surface"></a>デバイス管理の画面でテキストの描画

プラグインのレンダリングが Unidrv をフックする必要があります[ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277) (すべての他のグラフィックス DDI 描画関数) と共に関数。 デバイス管理の画面のテキストを作成するには、次の 4 つの関数間の相互作用が含まれます。

-   Unidrv の[ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)関数

-   プラグインのレンダリング[ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)フック関数

-   Unidrv の[ **IPrintOemDriverUni::DrvUniTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff553132)メソッド

-   プラグインのレンダリング[ **IPrintOemUni::TextOutAsBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff554277)メソッド

デバイス管理の画面でテキストを表示するために必要な手順は次のとおりです。

1.  GDI 呼び出し Unidrv の[ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)関数。

2.  Unidrv を呼び出す、レンダリング プラグインの[ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)関数をフックします。

3.  フック関数は、テキストのブラシ、回転、およびクリップ領域を指定するデバイスにコマンドを送信します。

4.  フック関数には、Unidrv の[ **IPrintOemDriverUni::DrvUniTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff553132)メソッドを使用するテキストを出力するフォントをダウンロードします。 このメソッドは、クリッピングのグリフに基づくも処理します。

5.  場合[ **IPrintOemDriverUni::DrvUniTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff553132) (フォントが利用できないか、回転) ために、ダウンロード可能なフォントを使用できません、呼び出し、レンダリング プラグインの[ **IPrintOemUni::TextOutAsBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff554277)メソッドで、ビットマップとしてテキストを描画します。

6.  後[ **IPrintOemDriverUni::DrvUniTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff553132)から制御が戻る、 [ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)下線を描画する必要があります関数をフックし、strike スルーがで指定された四角形に基づく、 **DrvTextOut**関数の*prclExtra* (サポートされている) 場合は、ベクターのコマンドを使用して、パラメーター。

 

 




