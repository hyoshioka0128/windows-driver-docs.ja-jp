---
title: リリース署名の概要
description: リリース署名の概要
ms.assetid: 87583d0a-f7c9-49f0-953a-f51891260d75
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aa5257be05265c900a5047f786ecd9c173817d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364299"
---
# <a name="introduction-to-release-signing"></a>リリース署名の概要


[ドライバー パッケージ](driver-packages.md)理由は次のリリース署名をする必要があります。

-   信頼性、整合性、およびドライバー パッケージの信頼性を確認してください。

    Windows は、発行元の身元を確認して、ドライバーが発行された後に変更されていないことを確認するにデジタル署名を使用します。

-   ドライバーの自動インストールを促進することで、最適なユーザー エクスペリエンスを提供します。

    ドライバーが署名されていない場合、[プラグ アンド プレイ (PnP) ドライバーのインストール ポリシー](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md)ことシステム管理者を手動で承認未署名のドライバのインストール、インストール プロセスには、追加手順を追加する必要があります。 この余分な手順は、可能性のあるわかりづらく、平均的なユーザーを特定できます。

-   64 ビット バージョンの Windows Vista と Windows の以降のバージョンでは、カーネル モード ドライバーを実行します。

    [カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md) Windows Vista 以降の 64 ビット バージョンのカーネル モード ドライバーは、オペレーティング システム、ドライバーの読み込みのために署名する必要があります。

-   特定の種類の次世代のプレミアム コンテンツを再生するには、Windows Vista および Windows の以降のバージョンですべてのカーネル モード コンポーネントに署名する必要があります。 さらに、すべてのユーザー モードとカーネル モード コンポーネント Protected Media Path (PMP) では、PMP の署名ポリシーに準拠する必要があります。 PMP については、ポリシーの署名のホワイト ペーパーを参照[Windows Vista のメディアの保護されているコンポーネントのコード署名](https://go.microsoft.com/fwlink/p/?linkid=69258)します。

[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)が[テスト カテゴリ](https://go.microsoft.com/fwlink/p/?linkid=189178)さまざまなデバイスの種類。 ドライバーの発行者を取得する必要があります、デバイスの種類のテスト カテゴリがこの一覧に含まれる場合、 [WHQL リリース署名](whql-release-signature.md)ドライバー パッケージ。

**注**  では、Windows Server 2003、Windows XP、および Windows 2000、WHQL 署名から INF ファイル[ドライバー パッケージ](driver-packages.md)を使用する必要があります、[デバイス セットアップ クラス](device-setup-classes.md)で定義されています。*%SystemRoot%/inf/Certclas.inf*します。 それ以外の場合、Windows は未署名としてドライバー パッケージを扱います。

 

WHQL によってデジタル署名されたドライバー パッケージの場合は、Windows 更新プログラムやその他の Microsoft でサポートされている配布メカニズムを通じて配布できます。 WHQL に署名するドライバー パッケージのカタログ ファイル (64 ビット プロセッサ向け)、ドライバーの発行者にもする必要があります[署名を埋め込む](embedded-signatures-in-a-driver-file.md)WHQL するドライバー パッケージを送信する前に、カーネル モード ドライバーのファイルにします。

場合、[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)はありません、[テスト カテゴリ](https://go.microsoft.com/fwlink/p/?linkid=189178)、デバイスの種類の次の種類のデジタル署名を使用する必要があります[リリース署名](release-signing-driver-packages.md)Windows Vista 以降のバージョンの Windows でドライバー パッケージ:

-   カーネル モード コード署名ポリシーを遵守するだけである、ドライバー パッケージの署名に[カタログ ファイル](catalog-files.md)します。 ブート開始ドライバーの場合、SPC 署名をカーネル モード ドライバーのファイルに埋め込むして、必要に応じて、ドライバー パッケージのカタログのファイルにも署名します。

-   準拠する、 [PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)SPC をいずれかを使用する 32 ビット バージョンの Windows Vista 以降のバージョンの Windows のまたは[コマーシャル リリースの証明書](commercial-release-certificate.md)署名に、カーネル モード ドライバー パッケージのカタログ ファイル。 これら後者の 2 つのシグネチャの型では、信頼性と整合性が、WHQL リリース署名とは異なり、ドライバーのドライバーの信頼性を検証しないことを確認します。

SPC と商用リリース証明書と総称されますとして[証明書をリリース](release-certificates.md)、リリースの証明書を使用して生成されたシグネチャと呼ばれる、*リリース署名*。

リリース署名の要件と手順の詳細については、次を参照してください。[ドライバー パッケージのリリース署名](release-signing-driver-packages.md)します。

**注**  ドライバー パッケージのリリースの署名に関連する手順については、次を参照してください。[リリース ドライバー パッケージを署名する方法](how-to-release-sign-a-driver-package.md)します。 このトピックでは、リリース署名プロセスの概要を提供し、リリース署名の例の多くを使用してステップ実行、 *ToastPkg*サンプル ドライバー パッケージ内で、Windows Driver Kit (WDK)。

 

 

 





