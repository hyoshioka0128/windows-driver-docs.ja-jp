---
title: ユーザー インターフェイス プラグインの概要
description: ユーザー インターフェイス プラグインの概要
ms.assetid: 7f01bd14-bcc5-4c26-a9b8-a12aa1ffe242
keywords:
- ユーザーインターフェイスプラグイン WDK print、ユーザーインターフェイスプラグインについて
- UI プラグイン WDK print、ユーザーインターフェイスプラグインについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a959ff4ff3164d97a68fd2951954c36f3f5785c
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461839"
---
# <a name="introduction-to-user-interface-plug-ins"></a>ユーザーインターフェイスプラグインの概要

新しいプリンターデバイスのサポートを[Microsoft Universal printer driver](microsoft-universal-printer-driver.md) (Unidrv) または[microsoft PostScript プリンタードライバー](microsoft-postscript-printer-driver.md) (pscript) のいずれかに追加する場合は、プリンターのプロパティシートまたはドキュメントのプロパティシートを変更することによって、ドライバーのユーザーインターフェイスをカスタマイズできます。

このカスタマイズは、ユーザーモードの DLL を提供することによって行います。 この DLL は、*ユーザーインターフェイスプラグイン*または*UI プラグイン*と呼ばれます。

UI プラグインは、プロパティシートの [**デバイス設定**] ページ内のオプションを追加、削除、または置換することで、プリンターのプロパティシートを変更できます。 新しいページを追加することもできます。 同様に、プラグインでは、プロパティシートの**レイアウト**、**用紙/品質**、および**詳細設定**ページ内のオプションを追加、削除、または置換することで、ドキュメントのプロパティシートを変更できます。また、新しいページを追加することもできます。

Windows Vista の Unidrv を使用している場合は、プラグインで[**IPrintOemUI2:: HideStandardUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui)メソッドを実装して、標準ドライバーが提供するすべてのプリンター構成プロパティページを非表示にすることができます。 プリンターに完全にカスタムのプリンター構成ユーザーインターフェイスを提供する場合は、この方法を使用できます。

> [!IMPORTANT]
> Windows ヘルプ (Winhlp32.exe) は、ユーザーが .hlp ファイルを表示できるようにするアプリケーションです。 Windows Vista 以降では、windows ヘルプアプリケーションは Windows オペレーティングシステムの一部として含まれていません。 .Hlp ファイルに依存するアプリケーションを開発するソフトウェア開発者は、ファイルを .chm、hxs、.html、.xml ファイルなどの代替のヘルプ形式に移行する必要があります。 詳細については、windows サポート技術情報の記事「 [Windows ヘルププログラム (winhlp32.exe)](https://go.microsoft.com/fwlink/p/?linkid=80917) 」を参照してください。

[プリンターインターフェイス DLL](printer-interface-dll.md)は、一連の COM インターフェイスを使用して、Unidrv または PSCRIPT の UI プラグインを呼び出します。 プリンターインターフェイス Dll は CPSUI を使用して実装され、UI プラグインは、ドライバーのプリンターインターフェイス DLL を介して間接的に CPSUI とやり取りします。 そのため、UI プラグインを開発する前に、 [CPSUI](common-property-sheet-user-interface.md)セクションを読む必要があります。

UI プラグインは、プリンタードライバーのユーザーインターフェイスを変更するだけでなく、特定のプリンターイベントの処理やサポートされている機能のレポートなど、その他の操作を実行できます。 詳細については、「[その他のプリンターインターフェイス操作のカスタマイズ](customizing-other-printer-interface-operations.md)」を参照してください。
