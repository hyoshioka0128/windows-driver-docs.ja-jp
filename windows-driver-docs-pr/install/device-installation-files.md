---
title: デバイスのインストール ファイル
description: デバイスのインストール ファイル
ms.assetid: a4a53040-ff53-49ba-a4a5-aba5f13119ef
keywords:
- デバイスのセットアップ WDK デバイスのインストール、ファイル
- デバイスのインストール WDK、ファイル
- WDK、ファイルのデバイスのインストール
- ファイル WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db76e33bee19d28014913ad1d517e31365ae155
ms.sourcegitcommit: f6aebb32c045b9da7da4bf9b3fd8d6fad05e9deb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77089211"
---
# <a name="device-installation-files"></a>デバイスのインストール ファイル





特定のデバイスをサポートするために必要なソフトウェアは、デバイスの種類とデバイスの使用方法によって異なります。 通常、ベンダーは、デバイスをサポートするために、次のソフトウェアを[ドライバーパッケージ](driver-packages.md)に提供します。

* <a href="" id="a-device-setup-information-file--inf-file-"></a>デバイスのセットアップ情報ファイル (INF ファイル)  
    INF ファイルには、システム Windows コンポーネントがデバイスのサポートをインストールするために使用する情報が含まれています。 Windows は、ドライバーをインストールするときに、このファイルを%*SystemRoot*%\\*inf*ディレクトリにコピーします。 このファイルは必須です。

    詳細については、「 [INF ファイルの作成](overview-of-inf-files.md)」を参照してください。

* <a href="" id="one-or-more-drivers-for-the-device"></a>デバイスの1つまたは複数のドライバー  
    ある.*sys*ファイルは、ドライバーのイメージファイルです。 ドライバーがインストールされると、Windows はこのファイルを *% SystemRoot%\\system32\\drivers*ディレクトリにコピーします。 ほとんどのデバイスにはドライバーが必要です。

    詳細については、「[ドライバーモデルの選択](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)」を参照してください。

* <a href="" id="digital-signatures-for-the-driver-package--a-driver-catalog-file-"></a>[ドライバーパッケージ](driver-packages.md)のデジタル署名 (ドライバーカタログファイル)  
    ドライバーカタログファイルには、デジタル署名が含まれています。 すべてのドライバーパッケージに署名する必要があります。

    ベンダーは、ドライバーパッケージをテストおよび署名のために Windows Hardware Quality Lab (WHQL) に送信することによって、デジタル署名を取得します。 WHQL は、カタログファイル () を含むパッケージを返します。*cat*ファイル)。

    詳細については、「 [WHQL リリース署名](whql-release-signature.md)」を参照してください。

* <a href="" id="other-files"></a>その他のファイル  
    [ドライバーパッケージ](driver-packages.md)には、カスタムデバイスインストールアプリケーション、デバイスアイコン、ドライバーライブラリファイル (ビデオドライバーなど) など、他のファイルを含めることができます。

    詳細については、「[特別なインストール要件を持つ](drivers-with-special-installation-requirements.md)[デバイスプロパティページ](providing-device-property-pages.md)とドライバーの提供」を参照してください。

また、WDK のデバイスタイプ固有のドキュメントも参照してください。

WDK には、さまざまなサンプルインストールファイルが含まれています。 詳細については、「[デバイスのインストールファイルの例](sample-device-installation-files.md)」を参照してください。

 

 





