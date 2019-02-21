---
title: Win 32 アプリケーションとの互換性を印刷チケット
description: Win 32 アプリケーションとの互換性を印刷チケット
ms.assetid: 3e358f8a-e950-4da0-b8ef-4e350ea28091
keywords:
- WDK の Win32 アプリケーションを印刷します。
- 印刷チケット WDK、Win32 アプリケーション
- 印刷チケット WDK、XPSDrv
- 印刷チケット WDK、GDI ベースの印刷ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af24bec9343a18fc82e34a07581453aa5a833dfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530025"
---
# <a name="print-ticket-compatibility-with-win-32-applications"></a>Win 32 アプリケーションとの互換性を印刷チケット


Microsoft Win32 ベースのアプリケーションと GDI ベースの印刷ドライバーでの印刷チケットを使用する場合は、次の互換性のシナリオを考慮する必要があります。

<a href="" id="win32-based-applications-that-are-printing-to-xpsdrv-print-drivers"></a>Win32 ベースのアプリケーションで XPSDrv に印刷するプリンター ドライバー  
ドキュメントの印刷チケットの対応する Win32 ベースのアプリケーションが XPSDrv プリンターのドライバーを印刷、GDI-XPS の変換モジュールは、Win32 ベースのアプリケーションが行う DDI 呼び出しから XPS スプール ファイルを作成します。 Windows Vista 印刷のサポートには、Win32 ベースのアプリケーションを使用し、ドキュメントの作成は XPS スプール ファイルに挿入しますの DEVMODE 構造体に基づく印刷チケットも作成します。 GDI-XPS 変換では、DEVMODE 構造体のパブリックな部分のみを変換できます。 変換には、適切な XML バイナリ エンコーディングを使用してバイナリ ラージ オブジェクト (BLOB) として印刷チケットにプライベート DEVMODE が埋め込まれます。 プライベート部分をバイナリの BLOB を復元することができます、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837) DEVMODEW に印刷チケットの変換で印刷チケットから構造体。

XPSDrv プリンター ドライバーには、Win32 ベースのアプリケーションから送信されるドキュメントでは、ドキュメントの両方が、XPS スプール ファイル形式でスプールされたため、Windows Presentation Foundation (WPF) アプリケーションから送信されるドキュメントとは異なる。

<a href="" id="wpf-applications-that-are-printing-to-gdi-based-print-drivers"></a>WPF アプリケーションに GDI ベース印刷をプリンター ドライバー  
Windows Vista 印刷のサポートが WPF アプリケーションに渡す XPS ドキュメントを変換する WPF アプリケーションは印刷チケットをサポートしていません GDI ベースの印刷ドライバーの印刷チケットを含むドキュメントを印刷する場合、 [EMF](emf-data-type.md)ファイルは、各印刷チケットの DEVMODE 構造体に変換します。

GDI 印刷ドライバーには、WPF アプリケーションから印刷ジョブは、Win32 アプリケーションを送信する印刷ジョブよりも違いではありません。

 

 




