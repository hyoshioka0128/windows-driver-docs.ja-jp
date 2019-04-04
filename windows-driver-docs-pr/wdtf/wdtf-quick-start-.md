---
title: WDTF のクイック スタート
description: Windows ドライバー キットは、作成、配置、および Windows ドライバー テスト フレームワーク (WDTF) を使用してテストを実行するための統合ソリューションを提供します。
ms.assetid: 77402D9A-DD21-4B7F-B052-43DB8C04EA1B
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: b076ac0ca2aba5175a03487db624b820c8aa605e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572550"
---
# <a name="wdtf-quick-start"></a>WDTF のクイック スタート

Windows ドライバー キットは、作成、配置、および Windows ドライバー テスト フレームワーク (WDTF) を使用してテストを実行するための統合ソリューションを提供します。 WDK を使用して、デプロイ、テスト、およびドライバーをデバッグするためのリモート コンピューターを構成できます。 リモート コンピューターを構成するときに、Windows ドライバー テスト フレームワーク ランタイムがインストールされます。

## <a name="installing-wdtf-runtime-library"></a>WDTF ランタイム ライブラリをインストールします。

### <a name="to-install-wdtf-runtime-library-using-visual-studio-and-the-wdk"></a>Visual Studio と WDK を使用して WDTF ランタイム ライブラリをインストールするには

1. Visual Studio をインストールし、WDK をインストールします。

2. テストおよびデプロイ用のリモート コンピューターを構成します。 Visual Studio での**ドライバー**メニューで、**テスト**順にクリックします**コンピューターを構成しています.**.

3. テスト コンピューターを構成するときに、Windows ドライバー テスト フレームワーク ランタイムがインストールされます。

- 詳細については、以下をご覧ください。

  - [テスト コンピューターへのドライバーの展開](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)

  - [ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)  

### <a name="installing-the-wdtf-runtime-library-manually"></a>WDTF ランタイム ライブラリを手動でインストールします。

WDK をインストールするときに、ドライバー テスト フレームワークの Windows ランタイムのインストール パッケージもインストールされます。 テスト コンピューターにインストール パッケージをコピーし、コマンドを実行する必要があります。 詳しくは、[テスト コンピューター (代替方法) WDTF ランタイム ライブラリを手動でインストール](https://docs.microsoft.com/windows-hardware/drivers/wdtf/wdtf-runtime-library#manually-installing-wdtf-on-a-test-computer-alternative-method)で、 [WDTF ランタイム ライブラリ](wdtf-runtime-library.md)を参照してください。

## <a name="writing-tests-with-wdtf"></a>WDTF を使用したテストの記述

WDK は、WDTF でテストを記述するためのテンプレートを提供します。 参照してください[ドライバー テスト テンプレートを使用してドライバーのテストを記述する方法](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-write-a-driver-test-)します。 ターゲット デバイスの WDTF 単純な I/O のプラグインを作成するのにテンプレートを使用することもできます。 詳しくは、[デバイス用のプラグイン WDTF 単純な I/O の書き込み](writing-a-wdtf-simpleio-plug-in-for-your-device.md)を参照してください。

## <a name="running-wdtf-tests"></a>WDTF テストの実行

WDTF ドライバー テスト テンプレートを使用して Visual Studio で、ドライバーのテストをビルドすると、新しいテストはテスト コンピューターに配置が可能になります。 既定では、作成したテストはテスト カテゴリの **[My Test Category] (個人用テスト カテゴリ)** に表示されます。 テストの名前は選択したテスト ケースに基づいたもので、**My Plug and Play Surprise Remove Test** のような名前になります。 各テストのビルド中に、テストは上書きされ、簡単にテストの実行機能で実行可能になります。 詳細については、[Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver-at-runtime)を参照してください。
