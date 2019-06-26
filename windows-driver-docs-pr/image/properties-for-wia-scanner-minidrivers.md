---
title: WIA スキャナー ミニドライバーのプロパティ
description: WIA スキャナー ミニドライバーのプロパティ
ms.assetid: 9de8694a-0d19-4945-b0c1-a3c4bc71dad3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54c4888ebb3eff9a2951f22886d7852dcc35b03
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374320"
---
# <a name="properties-for-wia-scanner-minidrivers"></a>WIA スキャナー ミニドライバーのプロパティ





次の一覧には、すべての WIA スキャナー ミニドライバーに固有の WIA プロパティが含まれます。

### <a name="required-properties-on-scanner-root-items-microsoft-windows-xp-and-windows-me"></a>スキャナーのルート項目のプロパティが必要です (Microsoft Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_光\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-optical-xres)

[**WIA\_DPS\_光\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-optical-yres)

### <a name="optional-properties-on-scanner-root-items-windows-xp-and-windows-me"></a>スキャナーの省略可能なプロパティはルート項目 (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_ディザー\_パターン\_データ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-dither-pattern-data)

[**WIA\_DPS\_ディザー\_を選択します**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-dither-select)

[**WIA\_DPS\_フィルター\_を選択します**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-filter-select)

[**WIA\_DPS\_最大\_スキャン\_時間**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-max-scan-time)

[**WIA\_DPS\_パッド\_色**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pad-color)

[**WIA\_DPS\_プラテン\_色**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-platen-color)

[**WIA\_DPS\_表示\_プレビュー\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-show-preview-control)

### <a name="required-properties-on-scanner-child-items-able-to-transfer-data"></a>スキャナーの子項目のデータを転送することが必要なプロパティ

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_IP\_明るさ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-brightness)

[**WIA\_IP\_コントラスト**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-contrast)

[**WIA\_IP\_CUR\_インテント**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-cur-intent)

[**WIA\_IP\_PHOTOMETRIC\_INTERP**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-photometric-interp)

[**WIA\_IP\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)

[**WIA\_IP\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)

[**WIA\_IP\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)

[**WIA\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)

[**WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)

[**WIA\_IP\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)

### <a name="optional-properties-on-scanner-child-items-able-to-transfer-data"></a>スキャナーの子項目のデータを転送することで、省略可能なプロパティ

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_ページ\_高さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-height)

[**WIA\_DPS\_ページ\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)

[**WIA\_DPS\_ページ\_幅**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-width)

[**WIA\_IP\_反転**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-invert)

[**WIA\_IP\_ミラー**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-mirror)

[**WIA\_IP\_向き**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation)

[**WIA\_IP\_回転**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation)

[**WIA\_IP\_しきい値**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)

[**WIA\_IP\_ウォーム\_を\_時間**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-warm-up-time)

### <a name="required-properties-on-flatbed-scanner-root-items-windows-xp-and-windows-me"></a>フラット ベッド スキャナーのルート項目のプロパティが必要です (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_水平\_ベッド\_登録**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-bed-registration)

[**WIA\_DPS\_水平\_ベッド\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-bed-size)

[**WIA\_DPS\_プレビュー**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-preview)

[**WIA\_DPS\_垂直\_ベッド\_登録**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-bed-registration)

[**WIA\_DPS\_垂直\_ベッド\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-bed-size)

### <a name="required-properties-on-document-feeder-scanner-root-items-windows-xp-and-windows-me"></a>ドキュメント フィーダー付きのスキャナー ルート項目のプロパティが必要です (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_ドキュメント\_処理\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)

[**WIA\_DPS\_ドキュメント\_処理\_を選択します**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)

[**WIA\_DPS\_ドキュメント\_処理\_状態**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)

[**WIA\_DPS\_水平\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-sheet-feed-size)

[**WIA\_DPS\_MIN\_水平\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-horizontal-sheet-feed-size)

[**WIA\_DPS\_MIN\_垂直\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-vertical-sheet-feed-size)

[**WIA\_DPS\_ページ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)

[**WIA\_DPS\_シート\_フィーダー\_登録**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-sheet-feeder-registration)

[**WIA\_DPS\_垂直\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-sheet-feed-size)

### <a name="properties-on-transparency-scanner-root-items-windows-xp-and-windows-me"></a>透過性スキャナーのプロパティ項目のルート (Windows XP と Windows Me)

WIA ミニドライバーは、次のプロパティを提供します。

[**WIA\_DPS\_透過性**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-transparency)

[**WIA\_DPS\_透明度\_を選択します**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-transparency-select)

 

 




