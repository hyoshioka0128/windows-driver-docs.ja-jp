---
title: デバイスのインストール アプリケーションの自動実行を開始
description: デバイスのインストール アプリケーションの自動実行を開始
ms.assetid: 9b520d82-2293-4936-99fe-30bf6753ba9f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79431a2febc178fe9d8e59c135adfa01f4cdc464
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536189"
---
# <a name="device-installation-application-started-through-autorun"></a>デバイスのインストール アプリケーションの自動実行を開始


このメソッドに既存の磨き[ソフトウェア最初インストール](software-first-installation.md)を作成する方法、[ハードウェア最初インストール](hardware-first-installation.md)シナリオ。 この方法では、 [ **INF HardwareId ディレクティブ**](inf-hardwareid-directive.md)、Windows Vista および Windows の以降のバージョンでサポートされています。

このメソッドで、*デバイス インストール アプリケーション*Autorun.inf ファイルの処理の一部としてのディストリビューションにメディアが起動します。 新しいハードウェアの検出ウィザードが、このファイルを解析し、検索、デバイス、ユーザーが接続されるときに、 [ **INF HardwareId ディレクティブ**](inf-hardwareid-directive.md)がインストールされているデバイスに一致します。 ウィザードには、一致が検出されると、インストールするデバイスの自動実行が有効なインストール アプリケーションを呼び出し、[ドライバー パッケージ](driver-packages.md)とデバイスに固有のアプリケーション。

このメソッドでは、次の利点があります。

-   独立系ハードウェア ベンダー (Ihv) は、このメソッドを追加して、既存の自動実行と互換性のある配布メディアを 1 つ以上に簡単に使用できます[ **INF HardwareId ディレクティブ**](inf-hardwareid-directive.md) Autorun.inf ファイルにします。 詳細については、自動実行とアプリケーションの自動実行が有効な[AutoRun-Enabled アプリケーションを作成する](https://go.microsoft.com/fwlink/p/?linkid=133162)を参照してください。

-   のみ、[ドライバー パッケージ](driver-packages.md)デジタル署名する必要があります。 デバイス インストールのアプリケーションと関連付けられているインストール ファイルは、デジタル署名するのにはありません。 デジタル署名の詳細については、[ドライバーの署名](driver-signing.md)を参照してください。

-   ドライバー パッケージのみがコピー、[ドライバー ストア](driver-store.md)します。 デバイス固有のアプリケーションは、ユーザーのハード ドライブに別の場所にインストールされます。

-   デバイスに固有のアプリケーションを更新するドライバー パッケージの更新中に、ユーザーを求められますことができます。 これは、を通して、[アクションのインストールが完了](finish-install-actions--windows-vista-and-later-.md)パッケージの共同インストーラーによって提供されます。 この方法では、ドライバー パッケージとデバイス固有のアプリケーションの更新プログラムを同期できます。 また、配布メディア上にない、またはその他の省略可能なアプリケーションは、インターネットからダウンロードできます。

ただし、このメソッドは、次の欠点もあります。

-   インストールするため、このメソッドを使用できます[ドライバー パッケージ](driver-packages.md)とデバイスに固有のアプリケーションのインストールでは、Windows Vista および Windows の以降のバージョンのみ。

-   配布メディアは、CD や DVD などの自動再生に対応である必要があります。 [ **INF HardwareId ディレクティブ**](inf-hardwareid-directive.md)インターネットからのアプリケーション インストーラーのダウンロードのすべての機能は提供されません。

 

 





