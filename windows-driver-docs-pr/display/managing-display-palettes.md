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
ms.openlocfilehash: 6bf6ad08d2da00edec66311c5428a3c5b89e750f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579674"
---
# <a name="managing-display-palettes"></a>ディスプレイ パレットの管理


## <span id="ddk_managing_display_palettes_gg"></span><span id="DDK_MANAGING_DISPLAY_PALETTES_GG"></span>


ビデオ ハードウェアは、設定できる色をサポートする場合と呼ばれる色ルックアップ テーブルを保持する*パレット*します。 GDI 各 RGB 値を受け取るし、デバイスに変換します*カラー インデックス*表示できるようにします。 GDI は、翻訳の事前計算済みおよびキャッシュされたテーブルを使用します。 ユーザー オブジェクトとこれらのテーブルがドライバーにアクセスできる[ **XLATEOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff570634)します。 そのため、すべての GDI グラフィックス関数を元の色を受け取り、ターゲット デバイスに移動しますは XLATEOBJ 構造を使用して、色を変換します。 パレットと GDI での処理方法の詳細については、次を参照してください。[パレットの GDI サポート](gdi-support-for-palettes.md)します。

ビデオ ハードウェアは、設定できるパレットをサポートする場合に、GDI が呼び出し、 **DrvSetPalette**アプリケーションによって要求されました。 GDI は、ディスプレイ ドライバーとドライバーのクエリに新しいパレットを渡す、 **PALOBJ**します。

*DrvSetPalette*関数を識別するハンドルを提供する、 *PDEV*ドライバーにし、そのデバイスのパレットを実現するドライバーを要求します。 ドライバーでは、特定のパレット内のエントリをできるだけ一致するようにハードウェア パレットを設定する必要があります。

デバイスを設定できますが、それ以外の場合は指定できませんパレットをサポートしている場合、このエントリ ポイントが必要です。 ディスプレイ ドライバーでは、そのデバイスが、GCAPS を設定して、設定可能なパレットを持つことを指定\_PALMANAGED ビット、 **flGraphicsCaps**のフィールド、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)返される構造体[ **DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)します。

サービス ルーチン[ **PALOBJ\_cGetColors** ](https://msdn.microsoft.com/library/windows/hardware/ff568845)ドライバーの表示に使用します。 この関数は、インデックス付きのパレットから RGB 色をダウンロードしの実装内から呼び出すことは*DrvSetPalette*します。

 

 





