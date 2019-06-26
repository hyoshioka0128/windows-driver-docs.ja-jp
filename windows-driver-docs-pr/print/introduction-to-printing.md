---
title: 印刷の概要
description: 印刷の概要
ms.assetid: 8a2e0151-6d40-493d-9757-42350a9e6220
keywords:
- WDK の印刷
- 表示コンポーネント WDK の印刷
- 構成コンポーネント WDK の印刷
- コンポーネントの WDK の印刷
- WDK の印刷のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 800cf423ac8629cd774555c02cb274deb6ac019a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385395"
---
# <a name="introduction-to-printing"></a>印刷の概要

Microsoft Windows 印刷アーキテクチャでは、印刷スプーラのプリンター ドライバーのセットで構成されます。 デバイス非依存関数を呼び出すことによってアプリケーションが印刷ジョブを作成し、多くのデバイスに送信できます。 レーザー プリンター場合は、にはこれが含まれていますプロッター、ラスターのプリンターをベクトルし、fax 装置。

プリンター ドライバーには、表示コンポーネントと構成コンポーネントが含まれます。 *表示コンポーネント*をプリンターがページ上のイメージを表示するために使用するデータ形式にアプリケーションからグラフィックス コマンドに変換します。 *構成コンポーネント*ユーザーがプリンターの選択可能なオプションとプリンターの構成と機能をアプリケーションに情報をやり取りするプログラム インターフェイスを制御できるようにするユーザー インターフェイス コンポーネントが含まれています。

Microsoft Win32 GDI アプリケーションを印刷するときは、Win32 API の GDI 関数を呼び出します。 これらの関数は、GDI グラフィックス エンジンへの情報を渡します。 GDI グラフィックス エンジンのいずれかのスプールとして描画命令、*拡張メタファイル (EMF)* ファイルまたはプリンター ドライバーをと共に、スプーラーに送信できる印刷可能なイメージを表示します。 スプーラー コンポーネントは、EMF ファイルを解釈し、ページ レイアウト情報およびジョブを制御する命令は、データ ストリームに挿入することができます。 スプーラは、データ ストリームにシリアル、パラレル、またはターゲットのプリンタの I/O ポートに関連付けられているネットワーク ポートのドライバーを送信します。 さらに、XPS 変換コンポーネントでは、GDI を介して GDI 印刷コマンドの場合は、XPS デバイスへの印刷、変換し、XPS 印刷パスの下に印刷ジョブを送信します。

XPS 印刷パスでは、プリンター ドライバーは XML Paper Specification (XPS) 上に基づきます。 Microsoft Win32 XPS アプリケーションを印刷するとき、アプリケーションは、XPS 印刷 API で XPS 関数を呼び出します。 キューへの印刷時[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md)スプーラーのレンダリングや出力デバイスに直接 XPS のスプール ファイルを渡します。 GDI のデバイスには、XPS ファイルを印刷する場合は、GDI 変換モジュールを XPS を通じて EMF ファイルに変換されます。 GDI の Win32 アプリケーションと同様の方法で GDI 印刷パスを通じて送信されます。

Windows Presentation Foundation (WPF) アプリケーションでは、XPS のスプール ファイル形式で、スプーラーに XPS ドキュメントをスプールする WPF の印刷のサポート関数を呼び出します。 ように、Win32 XPS アプリケーションからの印刷スプーラーが印刷キューに XPSDrv プリンター ドライバーを印刷するとき、スプーラーに元の形式でスプール ファイルが XPSDrv プリンター ドライバーのレンダリングやプリンターへの出力に渡されます。 GDI ベースになっているプリンターには、スプーラが印刷、バージョン 3 のプリンター ドライバーでは、スプーラー データを送信、XPS スプール ファイル形式で EMF ファイルへの変換については、GDI 変換モジュール。 データを印刷用の GDI ベースのプリンター ドライバーに送信します。 これらのデータ パスの詳細については、次を参照してください。 [Windows 印刷パスの概要](windows-print-path-overview.md)します。 XPS の詳細については、次を参照してください。、 [XML 仕様概要](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn641615(v=vs.85))します。

Spooler」および「ドライバー コンポーネントは、ハードウェア ベンダーが新しいハードウェアのサポートを簡単に追加できるように、置き換え可能な。 印刷スプーラとドライバー コンポーネントの詳細については、次のセクションを参照してください。

[印刷スプーラのアーキテクチャ](print-spooler-architecture.md)

[プリンター ドライバーのアーキテクチャ](printer-driver-architecture.md)

新しいプリンターのサポートは、通常、Microsoft から提供されたプリンター ドライバーのいずれかでのみ使用するための新しいデータ ファイルを作成する必要があります。 Microsoft のプリンター ドライバーの詳細については、次を参照してください。[プリンター ドライバーの概要](printer-driver-overview.md)します。

Microsoft ユニバーサル プリンター ドライバーと Microsoft Postscript プリンター ドライバーの動作をカスタマイズすることができます。 詳細については、次を参照してください。[をカスタマイズする Microsoft のプリンター ドライバー](customizing-microsoft-s-printer-drivers.md)します。 印刷スプーラをカスタマイズすることもできます。 詳細については、次を参照してください。[印刷スプーラー コンポーネントのカスタマイズ](print-spooler-components.md)します。

その他のセクションでは、次のトピックを説明します。

[ターミナル サーバーの印刷](terminal-server-printing.md)

[USB の印刷](usb-printing.md)

[Bluetooth の印刷](bluetooth-printing.md)

[プリンター ドライバーのテストとデバッグ](printer-driver-testing-and-debugging.md)
