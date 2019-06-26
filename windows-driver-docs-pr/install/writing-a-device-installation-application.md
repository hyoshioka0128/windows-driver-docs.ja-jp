---
title: デバイスのインストール アプリケーションの記述
description: デバイスのインストール アプリケーションの記述
ms.assetid: 9927e2e0-6c8e-437f-98ce-595bd304ec72
keywords:
- インストール アプリケーション WDK、インストール アプリケーションの作成方法
- インストール アプリケーションの作成に関するデバイス インストール アプリケーション WDK、
- インストール アプリケーションの作成、デバイス セットアップ WDK デバイス インストール
- デバイス インストール アプリケーションの作成、WDK をインストールします。
- デバイスのインストール アプリケーションの作成
- インストール アプリケーション WDK
- WDK のデバイス インストール アプリケーション
- アプリケーションの WDK デバイスのインストール
- デバイス WDK、アプリケーションのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e7bff2a6d3601234d40d5a5f931e4a88c7b999e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363496"
---
# <a name="writing-a-device-installation-application"></a>デバイスのインストール アプリケーションの記述





**注**  ユニバーサルまたはモバイルのドライバー パッケージでは、このセクションで説明する機能はサポートされていません。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

ドライバーをパッケージ化する場合は、これらのコンポーネントをインストールします。 デバイスのインストール アプリケーションと配布メディアは、自動実行が開始されるように、アプリケーションに自動的にユーザーが、配布メディアを挿入するときに、自動実行と互換性があります。 自動実行の詳細については、次を参照してください。 [AutoRun-Enabled アプリケーションを作成する](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/cc144206(v=vs.85))します。

デバイスのインストール アプリケーションを記述する方法に関するガイドラインについては、次を参照してください。[デバイス インストール アプリケーションの作成に関するガイドライン](guidelines-for-writing-device-installation-applications.md)します。

[ドライバー パッケージ](driver-packages.md)2 つの状況を処理する必要があります。

1.  ユーザーは、配布メディアを挿入する前に、ハードウェアに接続されます。 これはよく呼ば、[ハードウェア最初インストール](hardware-first-installation.md)します。

2.  ユーザーは、ハードウェアに接続する前に、配布メディアを挿入します。 これはよく呼ば、[ソフトウェア最初インストール](software-first-installation.md)します。

 

 





