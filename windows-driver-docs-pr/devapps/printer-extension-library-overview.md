---
title: UWP アプリのデバイスのプリンター拡張機能ライブラリの概要
description: このトピックでは、プリンターの拡張機能ライブラリでは、デバイスの製造元に役立つライブラリは、自社のプリンター用の UWP デバイス アプリを作成します。
ms.assetid: A47B17CE-BF5A-4C02-807C-890F315A13E0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d070674bac7259c6314aa1dd3df2d96bb3f6e7a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369364"
---
# <a name="printer-extension-library-overview-for-uwp-device-apps"></a>UWP アプリのデバイスのプリンター拡張機能ライブラリの概要


このトピックでは、プリンターの拡張機能ライブラリでは、デバイスの製造元に役立つライブラリは、自社のプリンター用の UWP デバイス アプリを作成します。 プリンターの拡張機能ライブラリに含まれている、[設定と印刷通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)サンプルとも、[ジョブの管理とプリンターの保守](https://go.microsoft.com/fwlink/p/?LinkID=299829)サンプル。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


高レベルの設計目標、 [v4 プリンター ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=314231)アーキテクチャは、Microsoft Store アプリのユーザー インターフェイスの組み込みサポートを提供することでした。 V4 印刷ドライバーが COM ベースを公開、プリンターへのアクセスを提供する[プリンター拡張機能インターフェイス](https://go.microsoft.com/fwlink/p/?LinkID=299887)します。

UWP デバイス アプリからそれらのインターフェイスにアクセスするには、デバイス アプリの Microsoft Store プリンター サンプルに含まれているプリンターの拡張機能ライブラリを使用することができます。 プリンターの拡張機能ライブラリは COM インターフェイスの COM の実装をラップ`PrinterExtensionLib`します。 これにより、コードのプリンター拡張と UWP デバイスのアプリ間で共有できます。

![プリンター拡張機能ライブラリの概要](images/373030-printer-app-architecture.png)

## <a name="span-idprinterextensionlibraryspanspan-idprinterextensionlibraryspanspan-idprinterextensionlibraryspanprinterextensionlibrary"></a><span id="PrinterExtensionLibrary"></span><span id="printerextensionlibrary"></span><span id="PRINTEREXTENSIONLIBRARY"></span>PrinterExtensionLibrary


プリンターのサンプルに含まれている PrinterExtensionLibrary プロジェクト内では、2 つC#ファイル。 これらのファイルは、PrinterExtensionLib の内容をラップします。 プリンターの拡張機能と UWP デバイス用アプリケーション間のコード共有を有効にするにはこのレイヤーで追加のクラスを追加する可能性があります。

-   **PrinterExtensionTypes.cs**の便利な列挙体、定数および COM PrinterExtensionLib Api をラップするインターフェイスの数を指定します。

-   **PrinterExtensionAdapters.cs** PrinterExtensionLib の COM Api をラップするために使用する constructable クラスのすべてを指定します。

補強できます。 このプロジェクトに必要なC#、プリンターの拡張機能や UWP デバイス アプリをビルドに必要な共通のモデルのレイヤーのコードを記述するファイル。 ただし、お勧めしません既存のクラスを更新するようにこれがより困難にサンプルに更新プログラムを利用したバグの修正を組み込むことです。

## <a name="span-iddeviceappforprinterslibraryspanspan-iddeviceappforprinterslibraryspanspan-iddeviceappforprinterslibraryspandeviceappforprinterslibrary"></a><span id="DeviceAppForPrintersLibrary"></span><span id="deviceappforprinterslibrary"></span><span id="DEVICEAPPFORPRINTERSLIBRARY"></span>DeviceAppForPrintersLibrary


DeviceAppForPrintersLibrary、という名前の追加のプロジェクトでは、ヘルパー クラスとメソッドを提供します。 C# UWP デバイス アプリからプリンターへのアクセスに使用できるアプリです。

## <a name="span-idprinterextensionhelperlibraryspanspan-idprinterextensionhelperlibraryspanspan-idprinterextensionhelperlibraryspanprinterextensionhelperlibrary"></a><span id="PrinterExtensionHelperLibrary"></span><span id="printerextensionhelperlibrary"></span><span id="PRINTEREXTENSIONHELPERLIBRARY"></span>PrinterExtensionHelperLibrary


変換するには、C#インターフェイス、クラスおよびメソッドを JavaScript でサポートされているものでは、このプロジェクトが WinMD ファイルに作成されます。 WinMD ファイルは、Windows ランタイム Api を指定します。 さらに、このライブラリは、利便性のオブジェクトを解析して、複数のアクティブ化のコンテキストや通知のトースト UI の作成など、Microsoft Store のデバイス アプリに固有の公開に使用できます。

-   **PrintHelperClass.cs**アプリでの JavaScript レイヤーに公開するために PrinterExtensionLibrary 名前空間が含まれています。 PrintTicket と双方向のいくつかの便利なメソッドも含まれています。

-   **PrinterNotificationHelper.cs** UI をトースト通知を表示する方法を示します。

**注**  、**出力の種類**でアセンブリを指定、PrinterExtensionHelperLibrary の**アプリケーション**プロジェクトのプロパティ ウィンドウのページ。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[V4 印刷ドライバーの開発](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[プリンター拡張機能インターフェイス (v4 印刷ドライバー)](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[ジョブの管理 (v4 プリンター ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/print/job-management)

[デバイスのメンテナンス (v4 プリンター ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/print/device-maintenance)

[双方向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP アプリの概要](getting-started.md)

[アプリを作成する UWP デバイス (ステップ バイ ステップ ガイド)](step-1--create-a-uwp-device-app.md)

[UWP デバイスのアプリ (ステップ バイ ステップ ガイド) のデバイス メタデータを作成します。](step-2--create-device-metadata.md)

 

 






