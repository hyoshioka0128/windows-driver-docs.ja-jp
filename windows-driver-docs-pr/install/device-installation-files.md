---
title: デバイスのインストール ファイル
description: デバイスのインストール ファイル
ms.assetid: a4a53040-ff53-49ba-a4a5-aba5f13119ef
keywords:
- デバイス セットアップ WDK デバイス インストールのファイル
- デバイスのインストール ファイル、WDK
- デバイス ファイル、WDK をインストールします。
- WDK デバイス インストール ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87958f2aa78b5161a5d710a5e81286c5bfeea46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549838"
---
# <a name="device-installation-files"></a>デバイスのインストール ファイル





特定のデバイスをサポートするために必要なソフトウェアは、デバイスとデバイスを使用する方法の種類によって異なります。 通常、仕入先はで、次のソフトウェアを提供します。、[ドライバー パッケージ](driver-packages.md)デバイスをサポートします。

<a href="" id="a-device-setup-information-file--inf-file-"></a>デバイスのセットアップ情報ファイル (INF ファイル)  
INF ファイルには、デバイスのサポートをインストールする Windows のシステム コンポーネントを使用する情報が含まれています。 Windows では、このファイルをコピー、%*SystemRoot*%\\*inf*ディレクトリ、ドライバーをインストールするとき。 このファイルが必要です。

詳細については、次を参照してください。 [INF ファイルを作成する](overview-of-inf-files.md)します。

<a href="" id="one-or-more-drivers-for-the-device"></a>デバイスの 1 つまたは複数のドライバー  
A。*sys*ファイルは、ドライバーのイメージ ファイル。 Windows には、このファイルのコピー、 *%systemroot%\\system32\\ドライバー*ディレクトリ、ドライバーがインストールされている場合。 ドライバーは、ほとんどのデバイスの必要があります。

詳細については、次を参照してください。[ドライバー モデルを選択する](https://msdn.microsoft.com/library/windows/hardware/ff554652)します。

<a href="" id="digital-signatures-for-the-driver-package--a-driver-catalog-file-"></a>デジタル署名、[ドライバー パッケージ](driver-packages.md)(ドライバー カタログ ファイル)  
ドライバー カタログのファイルには、デジタル署名が含まれています。 すべてのドライバー パッケージを署名する必要があります。

仕入先は、そのドライバー パッケージのテストと署名 Windows Hardware Quality Lab (WHQL) に送信することで、デジタル署名を取得します。 WHQL は、カタログ ファイルを使用して、パッケージを返します (.*cat*ファイル)。

詳細については、次を参照してください。 [WHQL リリース署名](whql-release-signature.md)します。

<a href="" id="other-files"></a>その他のファイル  
A[ドライバー パッケージ](driver-packages.md)カスタム デバイスのインストール アプリケーション、デバイスのアイコン、ドライバー ライブラリ ファイル (ビデオ ドライバーなど) などの他のファイルを含めることができます。

詳細については、次を参照してください。[デバイスのプロパティ ページを提供する](providing-device-property-pages.md)と[特別なインストール要件を持つドライバー](drivers-with-special-installation-requirements.md)します。

また、WDK でデバイス固有の種類のドキュメントを参照してください。

WDK には、さまざまなサンプルのインストール ファイルが含まれています。 詳細については、次を参照してください[デバイス インストール ファイルのサンプル。](sample-device-installation-files.md)

 

 





