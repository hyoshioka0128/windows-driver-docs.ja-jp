---
title: デバイスとドライバーのインストールのロードマップ
description: デバイスとドライバーのインストールのロードマップ
ms.assetid: d6cb6d8c-226f-4b6f-989a-36184236f826
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64dcc2012b2f19d98d683e7cf138c994dd5a1f5a
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136119"
---
# <a name="roadmap-for-device-and-driver-installation"></a>デバイスとドライバーのインストールのロードマップ


![コンパス、マップ、および指でマップ ポイントの図](images/map-hand-sml.png)

Windows オペレーティング システムでは、デバイスとドライバーをインストールするには、次の手順を実行します。

-   手順 1:Windows でのデバイスとドライバーのインストールの基礎について説明します。

    Windows ファミリのオペレーティング システムでのデバイスとドライバーのインストールの基本を理解する必要があります。 これは、適切な設計上の決定に役立てるため、され、開発プロセスを効率化できます。 詳細については、次を参照してください。[概要のデバイスとドライバーのインストール](overview-of-device-and-driver-installation.md)します。

-   手順 2:ドライバー パッケージとそのコンポーネントについて説明します。

    ドライバー パッケージは、デバイスをインストールして、Windows でサポートするに指定する必要がありますすべてのコンポーネントで構成されます。

    デバイスまたはドライバーをインストールするには、システムが提供して、ベンダーから提供されたコンポーネントがあります。 システムでは、すべてのデバイス クラスの汎用インストール ソフトウェアを提供します。 ベンダーは、ドライバー パッケージ内で 1 つまたは複数のデバイス固有のコンポーネントを提供する必要があります。

    詳細については、次を参照してください。[ドライバー パッケージ](driver-packages.md)します。

-   手順 3:情報 (INF) ファイルについて説明します。

    INF ファイルには、情報とデバイスの設定が含まれているシステム指定[デバイス インストールのコンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)インストールを使用して、[ドライバー パッケージ](driver-packages.md)デバイスやドライバーなどデバイス固有のアプリケーション。

    詳細については、次を参照してください。 [INF ファイル](inf-files.md)します。

-   手順 4:デバイスとドライバーのドライバー パッケージを作成します。

    ドライバー パッケージする必要があります、INF ファイル、デバイスのドライバー ファイル、されるだけでなく必要に応じて追加のソフトウェア コンポーネントを提供します。 コンポーネントに必要なドライバー パッケージを確認するには、サンプル トースター ドライバー パッケージを参照してください。

    ドライバー パッケージのコンポーネントに関する詳細については、次を参照してください。[ドライバー パッケージを作成する](https://docs.microsoft.com/windows-hardware/drivers/develop/creating-a-driver-package)します。

    ドライバー パッケージの詳細については、次を参照してください。、[トースター サンプル](https://docs.microsoft.com/windows-hardware/drivers/wdf/sample-kmdf-drivers)します。

-   手順 5:テスト署名には、ドライバーは、開発およびテスト中にパッケージ化します。

    参照のプレリリース版をサインインするとき、テスト証明書を使用するテスト署名、[ドライバー パッケージ](driver-packages.md)テスト コンピューターで使用します。 具体的には、これにより、開発者などの自己署名証明書を使用してドライバー パッケージの署名に、 [ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)ツールが生成されます。 この機能をインストールしてドライバー署名の検証が有効になっていると、Windows でドライバー パッケージをテストできます。

    詳細については、次を参照してください。[開発およびテスト中にドライバーの署名](signing-drivers-during-development-and-test.md)します。

- 手順 6:配布、ドライバー パッケージをリリース署名。

    テストおよび検証した後、[ドライバー パッケージ](driver-packages.md)リリース、ドライバー パッケージを署名する必要があります。 リリース署名ドライバー パッケージの発行元を識別します。 この手順は省略可能ですが、ドライバー パッケージはリリース署名は次の理由。

  - 信頼性、整合性、およびドライバー パッケージの信頼性を確認してください。 Windows は、発行元の身元を確認して、ドライバーが発行された後に変更されていないことを確認するにデジタル署名を使用します。
  - ドライバーの自動インストールを促進することで、最適なユーザー エクスペリエンスを提供します。
  - 64 ビット バージョンの Windows Vista と Windows の以降のバージョンでは、カーネル モード ドライバーを実行します。
  - 再生次世代のプレミアム コンテンツの特定の種類。

    [ドライバー パッケージ](driver-packages.md)はいずれかでリリース署名します。

  - A [WHQL リリース署名](whql-release-signature.md)経由で取得した、 [Windows ハードウェア互換性プログラム](https://docs.microsoft.com/windows-hardware/design/compatibility/)(用 Windows 10 の場合) または[Windows ハードウェア認定プログラム](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))(Windows 8 または 8.1 古いオペレーティング システム)。
  - 使って作成されたリリース署名、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)します。

    詳細については、次を参照してください。[パブリック リリース用のドライバーの署名](signing-drivers-for-public-release--windows-vista-and-later-.md)します。

- 手順 7:ドライバー パッケージを配布します。

    最後に、配布、[ドライバー パッケージ](driver-packages.md)します。 ドライバー パッケージがで定義されている品質基準を満たしているかどうか、 [Windows ハードウェア互換性プログラム](https://docs.microsoft.com/windows-hardware/design/compatibility/)(用 Windows 10 の場合) または[Windows ハードウェア認定プログラム](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))(for Windows 8/8.1 古いオペレーティング システム) を配布できます Microsoft Windows 更新プログラムを使用します。 詳細については、次を参照してください。[ドライバーを Windows Update に公開](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)します。

これらは、基本的な手順です。 追加の手順は、個々 のデバイスとドライバーのインストールのニーズに基づいて、必要でにあります。
