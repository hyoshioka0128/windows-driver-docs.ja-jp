---
title: Win 32 アプリケーションと印刷チケットの互換性
description: Win 32 アプリケーションと印刷チケットの互換性
ms.assetid: 3e358f8a-e950-4da0-b8ef-4e350ea28091
keywords:
- WDK の Win32 アプリケーションを印刷します。
- 印刷チケット WDK、Win32 アプリケーション
- 印刷チケット WDK、XPSDrv
- 印刷チケット WDK、GDI ベースの印刷ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfc7e75bf3d77f986b96514e3b72668cebb113b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363986"
---
# <a name="print-ticket-compatibility-with-win-32-applications"></a>Win 32 アプリケーションと印刷チケットの互換性


Microsoft Win32 ベースのアプリケーションと GDI ベースの印刷ドライバーでの印刷チケットを使用する場合は、次の互換性のシナリオを考慮する必要があります。

<a href="" id="win32-based-applications-that-are-printing-to-xpsdrv-print-drivers"></a>Win32 ベースのアプリケーションで XPSDrv に印刷するプリンター ドライバー  
ドキュメントの印刷チケットの対応する Win32 ベースのアプリケーションが XPSDrv プリンターのドライバーを印刷、GDI-XPS の変換モジュールは、Win32 ベースのアプリケーションが行う DDI 呼び出しから XPS スプール ファイルを作成します。 Windows Vista 印刷のサポートには、Win32 ベースのアプリケーションを使用し、ドキュメントの作成は XPS スプール ファイルに挿入しますの DEVMODE 構造体に基づく印刷チケットも作成します。 GDI-XPS 変換では、DEVMODE 構造体のパブリックな部分のみを変換できます。 変換には、適切な XML バイナリ エンコーディングを使用してバイナリ ラージ オブジェクト (BLOB) として印刷チケットにプライベート DEVMODE が埋め込まれます。 プライベート部分をバイナリの BLOB を復元することができます、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew) DEVMODEW に印刷チケットの変換で印刷チケットから構造体。

XPSDrv プリンター ドライバーには、Win32 ベースのアプリケーションから送信されるドキュメントでは、ドキュメントの両方が、XPS スプール ファイル形式でスプールされたため、Windows Presentation Foundation (WPF) アプリケーションから送信されるドキュメントとは異なる。

<a href="" id="wpf-applications-that-are-printing-to-gdi-based-print-drivers"></a>WPF アプリケーションに GDI ベース印刷をプリンター ドライバー  
Windows Vista 印刷のサポートが WPF アプリケーションに渡す XPS ドキュメントを変換する WPF アプリケーションは印刷チケットをサポートしていません GDI ベースの印刷ドライバーの印刷チケットを含むドキュメントを印刷する場合、 [EMF](emf-data-type.md)ファイルは、各印刷チケットの DEVMODE 構造体に変換します。

GDI 印刷ドライバーには、WPF アプリケーションから印刷ジョブは、Win32 アプリケーションを送信する印刷ジョブよりも違いではありません。

 

 




