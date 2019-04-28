---
title: ユーザー インターフェイス プラグインの概要
description: ユーザー インターフェイス プラグインの概要
ms.assetid: 7f01bd14-bcc5-4c26-a9b8-a12aa1ffe242
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、ユーザー インターフェイスのプラグインについて
- ユーザー インターフェイスのプラグインの詳細については、印刷 UI プラグインの WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ae0feca471cbaab42b958a8ae98e65918859654
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376918"
---
# <a name="introduction-to-user-interface-plug-ins"></a>ユーザー インターフェイス プラグインの概要





いずれかに新しいプリンター デバイスのサポートを追加すると、 [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md) (Unidrv) または[Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md) (Pscript) ドライバーのユーザーをカスタマイズすることができますプリンターのプロパティ シートまたはプリンターのドキュメントのプロパティ シートを変更することでインターフェイスです。

ユーザー モード DLL を提供することで、このカスタマイズを実現します。 この DLL と呼ばれます、*プラグインのユーザー インターフェイス*、または単*UI プラグイン*します。

プラグイン UI は、追加、削除、またはプロパティ シートの内のオプションを置換してプリンターのプロパティ シートを変更できます**デバイス設定**ページ。 新しいページを追加することもできます。 同様に、プラグインを変更できますドキュメントのプロパティ シートの追加、削除、またはプロパティ シートの内のオプションを置換して**レイアウト**、**用紙/品質**、および**詳細**ページ、またはそれには、新しいページを追加できます。

Windows Vista から Unidrv を使用している場合を実装できます、 [ **IPrintOemUI2::HideStandardUI** ](https://msdn.microsoft.com/library/windows/hardware/ff554142)メソッドですべてのプリンターの構成プロパティを非表示にするには、プラグインをページには、標準のドライバー提供します。 プリンターの完全なカスタムのプリンター構成ユーザー インターフェイスを提供する場合、このメソッドを使用することができます。

**重要な**  ユーザー .hlp ファイルを表示できるアプリケーションは、Windows ヘルプ (WinHlp32.exe)。 Windows Vista 以降、Windows ヘルプ アプリケーションが Windows オペレーティング システムの一部として含まれています。 、.Hlp ファイルに依存するアプリケーションを開発するソフトウェア開発者は、.chm、.hxs、.html、.xml ファイルなどの別のヘルプ形式のファイルを移行する必要があります。 詳細については、次を参照してください。、 [Windows ヘルプ プログラム (WinHlp32.exe) は Windows に付属しなく](https://go.microsoft.com/fwlink/p/?linkid=80917)サポート技術情報記事。

 

[プリンター インターフェイス DLL](printer-interface-dll.md)呼び出し UI プラグイン Unidrv または Pscript、COM インターフェイスのセットを使用します。 Dll が CPSUI、およびプラグインの UI を使用して実装されているプリンター インターフェイスと対話しない直接 CPSUI ドライバーのプリンター インターフェイス DLL を使用します。 そのため、必ず、 [CPSUI](common-property-sheet-user-interface.md)プラグイン UI を開発する前にセクションします。

だけでなく、プリンター ドライバーのユーザー インターフェイスを変更するには、プラグイン UI はサポートされている機能の特定のプリンター イベントを処理およびレポートなど、他の操作を実行できます。 詳細については、次を参照してください。[プリンター インターフェイスのその他の操作のカスタマイズ](customizing-other-printer-interface-operations.md)します。

 

 




