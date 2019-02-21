---
title: GPD で HP-GL/2 のベクター グラフィックス サポート (5e PCL) を有効にします。
description: GPD で HP-GL/2 のベクター グラフィックス サポート (5e PCL) を有効にします。
ms.assetid: 2ca5a2fe-4c37-4b7f-bd9b-d41240f8843f
keywords:
- HP-GL/2 モノクロ WDK Unidrv、サポートを有効にします。
- PCL 5e WDK Unidrv、サポートを有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04530d80df3245667c5d904e0c741d4b5a453a8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529824"
---
# <a name="enabling-hp-gl2-vector-graphics-support-pcl-5e-in-the-gpd"></a>GPD で HP-GL/2 のベクター グラフィックス サポート (5e PCL) を有効にします。





Windows XP で HP-GL/2 ベクトルのサポートを有効にするには、2 つのことを行う必要があります。

1.  設定、 **\*パーソナリティ**属性パーソナリティを\_HPGL2 します。

2.  HPGL2MODE オプションがあります、GraphicsMode カスタマイズされた機能を定義します。 ラスター グラフィックス サポートを提供するには、RASTERMODE オプションが含まれます。

この方法では、性格属性を設定できます。

```cpp
*Personality: =PERSONALITY_HPGL2
```

パーソナリティ\_stdnames.gpd で HPGL2 定数が定義されています。

設定 GPD の次の例に示します、 \***パーソナリティ**属性と、ベクター グラフィックス モードとラスター グラフィックスのモードの両方で GraphicsMode カスタマイズされた機能を定義します。 注ブロック全体がによって保護されている、 \*Ifdef GPD コンパイラ ディレクティブ。

```cpp
*Ifdef: WINNT_51
*Personality: =PERSONALITY_HPGL2
*Feature: GraphicsMode
{
    *rcNameID: =GRAPHICSMODE_DISPLAY
    *FeatureType: DOC_PROPERTY
    *HelpIndex: 12000
    *DefaultOption: HPGL2MODE
    *Option: HPGL2MODE
    {
        *rcNameID: =GRAPHICSMODE_HPGL2_DISPLAY
    }
    *Option: RASTERMODE
    {
        *rcNameID: =GRAPHICSMODE_RASTER_DISPLAY
    }
}
*Endif:
```

WINNT\_51 のパラメーターが上記のディレクティブで使用されているオペレーティング システムのバージョンではなく Unidrv のバージョンに適用されます。 Windows 2000 では、WINNT で実行されている Windows XP Unidrv プリンター ドライバーの\_51 パラメーターが定義されており、ブロックがコンパイルされます。 オペレーティング システムのバージョンに関係なく、Unidrv の以前のバージョンのこのパラメーターが定義されていないと、ブロックはコンパイルされません。

次の一般的な例で示すように返さ機能では、カラー プリンターの GPD ファイルを定義することがもあります。 プリンターの具体的な詳細では、特定の値に変更される場合がありますに注意してください。

```cpp
*Feature: ColorMode
{
  *rcNameID: =COLOR_PRINTING_MODE_DISPLAY
  *HelpIndex: 12004
  *DefaultOption: 24bpp
  *Option: Mono
   {
     *rcNameID: =MONO_DISPLAY
     *DevNumOfPlanes: 1
     *DevBPP: 1
     *Color?: FALSE
     *Command: CmdSelect
      {
        *Order: PAGE_SETUP.16 
        *Cmd: "<1B>&b1M"
      }
   }
  *Option: 24bpp
   {
     *rcNameID: =24BPP_DISPLAY
     *DevNumOfPlanes: 1
     *DevBPP: 24
     *DrvBPP: 24
     *PaletteSize: 256
     *PaletteProgrammable?: TRUE
     *Command: CmdDefinePaletteEntry
      {
        *Cmd : "<1B>*v" %d{RedValue}"a"
+                       %d{GreenValue}"b"
+                       %d{BlueValue}"c"
+                       %d{PaletteIndexToProgram}"I"
 }
     *Command: CmdSelectPaletteEntry { *Cmd : "<1B>*v" 
+                        %d{CurrentPaletteIndex}"S" }
     *Command: CmdSetSrcBmpWidth { *Cmd : "<1B>*r" 
+                        %d{RasterDataWidthInBytes / 3}"S" }
     *Command: CmdSelect
      {
        *Order: PAGE_SETUP.16
        *Cmd: "<1B>*v1N<1B>*v1O<1B>*l184O<1B>*v6W<000308080808>
+              <1B>*v0a0b0c7i255a255b255c"
      }
   }
}
```

 

 




