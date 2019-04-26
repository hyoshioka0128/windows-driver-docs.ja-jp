---
title: WIA スキャナー ミニドライバーのプロパティ
description: WIA スキャナー ミニドライバーのプロパティ
ms.assetid: 9de8694a-0d19-4945-b0c1-a3c4bc71dad3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e65de5eca5a7ff0d4f2182743d1b4234640d7e57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355339"
---
# <a name="properties-for-wia-scanner-minidrivers"></a>WIA スキャナー ミニドライバーのプロパティ





次の一覧には、すべての WIA スキャナー ミニドライバーに固有の WIA プロパティが含まれます。

### <a name="required-properties-on-scanner-root-items-microsoft-windows-xp-and-windows-me"></a>スキャナーのルート項目のプロパティが必要です (Microsoft Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_光\_XRES**](https://msdn.microsoft.com/library/windows/hardware/ff551409)

[**WIA\_DPS\_光\_YRES**](https://msdn.microsoft.com/library/windows/hardware/ff551410)

### <a name="optional-properties-on-scanner-root-items-windows-xp-and-windows-me"></a>スキャナーの省略可能なプロパティはルート項目 (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_ディザー\_パターン\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551376)

[**WIA\_DPS\_ディザー\_を選択します**](https://msdn.microsoft.com/library/windows/hardware/ff551377)

[**WIA\_DPS\_フィルター\_を選択します**](https://msdn.microsoft.com/library/windows/hardware/ff551392)

[**WIA\_DPS\_最大\_スキャン\_時間**](https://msdn.microsoft.com/library/windows/hardware/ff551403)

[**WIA\_DPS\_パッド\_色**](https://msdn.microsoft.com/library/windows/hardware/ff551412)

[**WIA\_DPS\_プラテン\_色**](https://msdn.microsoft.com/library/windows/hardware/ff551420)

[**WIA\_DPS\_表示\_プレビュー\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff551432)

### <a name="required-properties-on-scanner-child-items-able-to-transfer-data"></a>スキャナーの子項目のデータを転送することが必要なプロパティ

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_IP\_明るさ**](https://msdn.microsoft.com/library/windows/hardware/ff552567)

[**WIA\_IP\_コントラスト**](https://msdn.microsoft.com/library/windows/hardware/ff552573)

[**WIA\_IP\_CUR\_インテント**](https://msdn.microsoft.com/library/windows/hardware/ff552579)

[**WIA\_IP\_PHOTOMETRIC\_INTERP**](https://msdn.microsoft.com/library/windows/hardware/ff552640)

[**WIA\_IP\_XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)

[**WIA\_IP\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)

[**WIA\_IP\_XRES**](https://msdn.microsoft.com/library/windows/hardware/ff552665)

[**WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)

[**WIA\_IP\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)

[**WIA\_IP\_YRES**](https://msdn.microsoft.com/library/windows/hardware/ff552673)

### <a name="optional-properties-on-scanner-child-items-able-to-transfer-data"></a>スキャナーの子項目のデータを転送することで、省略可能なプロパティ

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_ページ\_高さ**](https://msdn.microsoft.com/library/windows/hardware/ff551416)

[**WIA\_DPS\_ページ\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551417)

[**WIA\_DPS\_ページ\_幅**](https://msdn.microsoft.com/library/windows/hardware/ff551419)

[**WIA\_IP\_反転**](https://msdn.microsoft.com/library/windows/hardware/ff552599)

[**WIA\_IP\_ミラー**](https://msdn.microsoft.com/library/windows/hardware/ff552616)

[**WIA\_IP\_向き**](https://msdn.microsoft.com/library/windows/hardware/ff552625)

[**WIA\_IP\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff552648)

[**WIA\_IP\_しきい値**](https://msdn.microsoft.com/library/windows/hardware/ff552655)

[**WIA\_IP\_ウォーム\_を\_時間**](https://msdn.microsoft.com/library/windows/hardware/ff552660)

### <a name="required-properties-on-flatbed-scanner-root-items-windows-xp-and-windows-me"></a>フラット ベッド スキャナーのルート項目のプロパティが必要です (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_水平\_ベッド\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff551398)

[**WIA\_DPS\_水平\_ベッド\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551399)

[**WIA\_DPS\_プレビュー**](https://msdn.microsoft.com/library/windows/hardware/ff551422)

[**WIA\_DPS\_垂直\_ベッド\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff551442)

[**WIA\_DPS\_垂直\_ベッド\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551445)

### <a name="required-properties-on-document-feeder-scanner-root-items-windows-xp-and-windows-me"></a>ドキュメント フィーダー付きのスキャナー ルート項目のプロパティが必要です (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_ドキュメント\_処理\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551379)

[**WIA\_DPS\_ドキュメント\_処理\_を選択します**](https://msdn.microsoft.com/library/windows/hardware/ff551384)

[**WIA\_DPS\_ドキュメント\_処理\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff551386)

[**WIA\_DPS\_水平\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551401)

[**WIA\_DPS\_MIN\_水平\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551405)

[**WIA\_DPS\_MIN\_垂直\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551407)

[**WIA\_DPS\_ページ**](https://msdn.microsoft.com/library/windows/hardware/ff551414)

[**WIA\_DPS\_シート\_フィーダー\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff551430)

[**WIA\_DPS\_垂直\_シート\_フィード\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551446)

### <a name="properties-on-transparency-scanner-root-items-windows-xp-and-windows-me"></a>透過性スキャナーのプロパティ項目のルート (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_透過性**](https://msdn.microsoft.com/library/windows/hardware/ff551434)

[**WIA\_DPS\_透明度\_を選択します**](https://msdn.microsoft.com/library/windows/hardware/ff551437)

 

 




