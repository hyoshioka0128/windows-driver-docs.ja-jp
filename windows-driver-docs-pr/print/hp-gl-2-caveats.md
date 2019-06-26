---
title: HP-GL/2 注意事項
description: HP-GL/2 注意事項
ms.assetid: 201a894e-5d22-46f8-965d-0e5b88dc54d7
keywords:
- HP-GL/2 モノクロ WDK Unidrv、追加の考慮事項
- PCL 5e WDK Unidrv、追加の考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394529ca3723c5cf127ec36efb7f1d5fdabef2cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373812"
---
# <a name="hp-gl2-caveats"></a>HP-GL/2 注意事項





1.  HP-GL/2 は、Windows XP を備えた Unidrv に付属していると (Windows XP Unidrv と Windows XP - 問い合わせて、unidrvui.dll、unires.dll、および stdnames.gpd に付属するドライバー ファイルのセットを指します) 以降のオペレーティング システム リリースのバージョンに対してのみ機能します。 Windows 2000 Unidrv では機能しません。 Unidrv の Windows XP のバージョンが (たとえば、Windows 2000 マシンは、ポイントと Windows Server 2003 以降を実行しているコンピューターへの接続を印刷)、Windows 2000 を実行するマシン上に存在する場合は、ドライバーは HP-GL/2 を使用します。

2.  GPD レンダリング コマンドの一部には、HP-GL/2 モードがアクティブな場合は無視されます。 代わりに、ドライバーでハード コーディングされたコマンドが使用されます。 ただし、これらのコマンドは、次の理由で、GPD で存在する必要があります。
    1.  以降のバージョンのオペレーティング システムでは、レンダリング コマンドのハード コーディングが削除されます。
    2.  HP-GL/2 のドライバーがラスター モードに切り替えるオプションを提供しています (つまり、HP-GL/2 のドライバーを使用しない)。 ラスター モードの場合、GPD に存在するすべてのコマンドがあります。

        適切な経験則は、実際に何か (たとえば、CmdDownloadPattern または CmdSelectBlackBrush) を描画するために使用される任意の PCL-XL/HP-GL/2 コマンドは無視されることです。 コマンドが描画されるページ設定、ドキュメントのセットアップ、およびその他のユーザーなどのコマンドは無視されません。 これらのコマンドの詳細については、次を参照してください。[色コマンド](color-commands.md)します。

        さらに、HP-GL/2 のすべてのコマンドは、ドライバーでハードコードします。

3.  マスクへの呼び出しで受け取った[ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)しその他のビット ブロック転送機能が正しく動作しない可能性があります。

4.  Windows XP Unidrv が Windows 2000 で使用すると、HP-GL/2 をアクティブ化、一部のグラフィックスのレンダリング関数が正しく動作しない可能性があります。 出力例: [ **DrvGradientFill** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)呼び出しが赤、青が逆になります。

5.  Unidrv では、プリンターのハードウェアが ROP コマンドをサポートしていることを前提としています。 プリンターが ROP をサポートしていない場合、いくつかのドキュメントが正しく印刷されない可能性があります。

6.  ハッチ ブラシのサポートが必要です。 プリンターがハッチ ブラシをサポートしていない場合、出力は、プリンターのハードウェアが、ハッチ ブラシの選択コマンド (FT21, x SV21, x) を処理する方法に依存します。

7.  モノクロ プリンター ハッチ ブラシの色は無視されます。 常に黒で印刷されます。

8.  カラー プリンター、HP-GL/2 のみ 24 bpp/600 dpi をサポートします。 モノクロ プリンターは、HP-GL/2 では、600 dpi のみをサポートしています。 プリンターでは、その他の値をサポートする場合は、HP-GL/2 され場合にのみ色深度が 24 ビット/ピクセルの解像度は 600 dpi を選択するモードを制限します。 次の例では、GraphicsMode 機能を変更して、これを実現する方法を示します。 この例では、最初の\*制約のエントリが Unidrv Option2 値の解決の機能が 600 x 600 dpi である場合は、HPGL2MODE にモードの変更を拒否します。 (例では、前提 Option2 値が 300 x 300 dpi など、いくつかの低解像度である。)2 番目の\*制約のエントリが Unidrv 返さ機能のオプションは、色または 8bpp 場合モードの変更を拒否します。
    ```cpp
    *Feature: GraphicsMode
    {
      *rcNameID: =GRAPHICSMODE_DISPLAY
      *FeatureType: DOC_PROPERTY
      *HelpIndex: 12000
      *DefaultOption: HPGL2MODE
      *Option: HPGL2MODE
       {
         *rcNameID: =GRAPHICSMODE_HPGL2_DISPLAY
         *Constraints: Resolution.Option2
         *Constraints: LIST(ColorMode.Color, ColorMode.8bpp)
       }
      *Option: RASTERMODE
       {
         *rcNameID: =GRAPHICSMODE_RASTER_DISPLAY
       }
    }
    ```

9.  カラー プリンターは、イメージをスケーリングするハードウェアでできる必要があります。 この要件は、モノクロ プリンターは存在しません。

10. 、モノクロ プリンターのいると見なされます。
    -   プリンターでは、1bpp 情報のみを受け入れます。
    -   1 に設定されたビットは黒のピクセルを示し、0 に設定されたビットが白のピクセルを示します。
    -   灰色のことはできません、プリンターの任意の色をスケーリングします。 (これに起因自然 1 bpp 制限します。)

11. 次の圧縮方法をサポートする必要があります。
    -   圧縮なし
    -   TIFF
    -   デルタ行

12. HP-GL/2 では、システム ランドス ケープのローテーションは実行されません。 HP-GL/2 が有効にすると、プリンターがラスター、フォント、および横モードで印刷されるページの座標の回転を処理すると見なされます。 この問題に対処することを確認します GPD 回転のすべてのパラメーター (、 \*RotateCoordinate ですか?、 \*RotateFont ですか?、および\*RotateRaster でしょうか。 属性) に設定されます**TRUE**。 いない HP GL/2 をアクティブ化またはメモリの制約を配置することを検討してください、プリンターに回転がメモリのオーバーフローの問題がある場合 (つまり、HP-GL/2 をアクティブ化するメモリが 4 MB 以上の場合のみです。

    メモリ不足のデバイス (たとえば、600 dpi モノクロ レーザー プリンターでは、2 MB の RAM) で、デバイスが HP-GL/2 モードの場合は、メモリ不足のエラーを生成する特定のページは可能性がありますラスター モードで正しく印刷します。 メモリの完全なビットマップより少ないデバイスの 1 つのソリューションは、ラスター モードでは、既定値は、GPD を記述して、システムが HP-GL/2 ではなく、横置きに回転を処理できるようにするには。 さらに、特定の複雑な縦の印刷ジョブは可能性がありますラスター モードでは、HP-GL/2 のモードではなく、正しく印刷します。 場合は、ラスター モード、既定のことを検討してください。

13. 印刷の最適化機能、**詳細**HP-GL/2 のモードでプリンターのプロパティ ページのタブは、現在は無視されます。

14. \*MirrorRasterPage でしょうか。HP-GL/2 のモードではサポートされません。

15. ラスター フォント GPD ファイルで指定して、デバイスをサポートしている場合でもアウトライン フォントとしてダウンロードする TrueType アウトライン フォントのことができます。 これは、さまざまな理由 (たとえば、プリンターの不十分なメモリ) 発生することができます。

 

 




