---
title: PCL XL ミニドライバーの色のサポートを有効にする
description: PCL XL ミニドライバーの色のサポートを有効にする
ms.assetid: 3287b070-76e3-4a28-a516-aa58905af224
keywords:
- PCL XL ベクター グラフィックス WDK Unidrv、色のサポートを有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6310152a031f798dcec7035d6a5e759a3fee3c98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378617"
---
#  <a name="enabling-support-for-color-in-pcl-xl-minidrivers"></a>PCL XL ミニドライバーの色のサポートを有効にする





PCL XL の色の GPD ファイルの開発は、モノクロの PCL XL GPD ファイルの開発に似ています。 このトピックでは、主な相違点を説明します。 ここで紹介するサンプル GPD エントリは、デバイスに適切に変更する必要があります。

-   GPD ファイルは、デバイスでは色が指定する必要があります。

    つまり、GPD ファイルは、返さを含める必要があります[の標準機能](standard-features.md)します。 PCL XL の現在の実装が 24 ビット/ピクセルの色のみをサポートしていることに注意してください。 次の例では、2 つ含まれる返さ機能\*エントリのオプションします。Mono と 24 bpp の色。

```cpp
*Feature: ColorMode
{
    *rcNameID: =COLOR_PRINTING_MODE_DISPLAY
    *DefaultOption: 24bpp
    *Option: Mono
    {
        *rcNameID: =MONO_DISPLAY
        *DevNumOfPlanes: 1
        *DevBPP: 24
        *DrvBPP: 24
        *Color? : FALSE
        *PaletteSize: 1
        *PaletteProgrammable? : TRUE
        *Command: CmdDefinePaletteEntry { *Cmd: "" }
    }
    *Option: 24bpp
    {
        *rcNameID: =24BPP_DISPLAY
        *DevNumOfPlanes: 1
        *DevBPP: 24
        *DrvBPP: 24
        *PaletteSize: 256
        *PaletteProgrammable? : TRUE
        *Command: CmdDefinePaletteEntry { *Cmd: "" }
    }
}
```

-   いくつかのコマンドは、カラー印刷用に変更する必要があります。

    たとえば、GPD ファイルは、ユーザーが印刷の色と (前の例では) とモノクロの選択を許可している場合、ページのセットアップのコマンドは白黒またはカラーにユーザーを印刷するかどうかに依存のようになります。 この場合、 **CmdStartPage**コマンド (を参照してください[プリンター構成コマンド](printer-configuration-commands.md)) 内に配置する必要があります、\*スイッチ。次の例に示す返さステートメント。 (なおで数値 4、\*順序。ページ\_SETUP.4 コマンドの属性が GPD ファイルとデバイスに応じて、変更する必要があります)。ページの詳細については\_構文をセットアップしを参照してください[コマンドの実行順序](command-execution-order.md)します。

```cpp
*Switch: ColorMode
{
  *Case: Mono
  {
    *Command: CmdStartPage
    {
    *Order: PAGE_SETUP.4
    *Cmd: =real32_xy "<0000803f><0000803f>" =attr_ubyte =PageScale =SetPageScale
+         =ubyte =eGray =attr_ubyte =ColorSpace =SetColorSpace
    }
  }
  *Case: 24bpp
  {
    *Command: CmdStartPage
    {
    *Order: PAGE_SETUP.4
    *Cmd: =real32_xy "<0000803f><0000803f>" =attr_ubyte =PageScale =SetPageScale
+         =ubyte =eRGB =attr_ubyte =ColorSpace =SetColorSpace
    }
  }
}
```

-   いくつかのコマンドまたは、GPD モノクロ デバイスに提供される情報は、削除または変更する必要があります。

    たとえば、色の情報を追加するには、p6sample.gpd サンプル GPD ファイルを変更する場合があります削除する、\*機能。ディザー[カスタマイズされた機能](customized-features.md)モノクロ モードで印刷する場合にのみが使用されるように制限できますか。

 

 




