---
title: ディスプレイ パレットの管理
description: ディスプレイ パレットの管理
ms.assetid: a0ff1a9c-82dc-4317-a0ec-c387027a52ba
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、パレット
- 色のルックアップ テーブル WDK Windows 2000 の表示
- Windows 2000 の WDK のパレットを表示します。
- Windows 2000 の WDK のカラー パレットを表示します。
- Windows 2000 の WDK 表示の色のインデックス
- 設定可能なパレット WDK Windows 2000 を表示します。
- インデックス付きパレット WDK Windows 2000 を表示します。
- Windows 2000 の WDK の RGB 色を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f894a6d31b517d7b8e26998c652ee253ef462a55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382307"
---
# <a name="managing-display-palettes"></a>ディスプレイ パレットの管理


## <span id="ddk_managing_display_palettes_gg"></span><span id="DDK_MANAGING_DISPLAY_PALETTES_GG"></span>


ビデオ ハードウェアは、設定できる色をサポートする場合と呼ばれる色ルックアップ テーブルを保持する*パレット*します。 GDI 各 RGB 値を受け取るし、デバイスに変換します*カラー インデックス*表示できるようにします。 GDI は、翻訳の事前計算済みおよびキャッシュされたテーブルを使用します。 ユーザー オブジェクトとこれらのテーブルがドライバーにアクセスできる[ **XLATEOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)します。 そのため、すべての GDI グラフィックス関数を元の色を受け取り、ターゲット デバイスに移動しますは XLATEOBJ 構造を使用して、色を変換します。 パレットと GDI での処理方法の詳細については、次を参照してください。[パレットの GDI サポート](gdi-support-for-palettes.md)します。

ビデオ ハードウェアは、設定できるパレットをサポートする場合に、GDI が呼び出し、 **DrvSetPalette**アプリケーションによって要求されました。 GDI は、ディスプレイ ドライバーとドライバーのクエリに新しいパレットを渡す、 **PALOBJ**します。

*DrvSetPalette*関数を識別するハンドルを提供する、 *PDEV*ドライバーにし、そのデバイスのパレットを実現するドライバーを要求します。 ドライバーでは、特定のパレット内のエントリをできるだけ一致するようにハードウェア パレットを設定する必要があります。

デバイスを設定できますが、それ以外の場合は指定できませんパレットをサポートしている場合、このエントリ ポイントが必要です。 ディスプレイ ドライバーでは、そのデバイスが、GCAPS を設定して、設定可能なパレットを持つことを指定\_PALMANAGED ビット、 **flGraphicsCaps**のフィールド、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)返される構造体[ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)します。

サービス ルーチン[ **PALOBJ\_cGetColors** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors)ドライバーの表示に使用します。 この関数は、インデックス付きのパレットから RGB 色をダウンロードしの実装内から呼び出すことは*DrvSetPalette*します。

 

 





