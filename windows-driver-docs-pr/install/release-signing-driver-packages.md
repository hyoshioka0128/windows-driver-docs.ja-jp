---
title: ドライバー パッケージのリリース署名
description: ドライバー パッケージのリリース署名
ms.assetid: 57125c3b-55f0-4b60-b4d9-1408e26faccb
keywords:
- ドライバー WDK、ドライバー パッケージの署名
- ドライバー WDK、ドライバー パッケージの署名
- WDK、ドライバー パッケージのデジタル署名
- WDK、ドライバー パッケージの署名
- CAT ファイル
- .cat ファイル
- カタログ ファイル WDK ドライバーの署名、署名をリリース
- パブリック リリース ドライバーのリリースの署名について、WDK を署名
- リリースのリリースの署名について、WDK を署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdac7632ebb4ca2a2ce85a8deaa501051d56abbf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387312"
---
# <a name="release-signing-driver-packages"></a>ドライバー パッケージのリリース署名


このセクションに Windows Vista および Windows の以降のバージョンのリリース用のドライバーに署名するコンピューターを参照として、*コンピューターを署名*します。 署名のコンピューターでは、Windows XP SP2 または Windows オペレーティング システムの以降のバージョンが実行されている必要があります。 など、ドライバーを Windows 7 のリリースのためのものでは、Windows Vista を実行しているコンピューターで署名できます。

さらに、署名のコンピューターが必要、[ドライバーの署名ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-signing-drivers)をインストールします。

**注**  のバージョンを使用する必要があります、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool) Windows Vista およびそれ以降のバージョンの Windows Driver Kit (WDK) で提供されるツールです。 このツールの以前のバージョンでは、署名ポリシーを Windows Vista 以降のバージョンの Windows カーネル モード コードはサポートされません。

 

準拠する、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)と[プラグ アンド プレイ (PnP) デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)Windows Vista 以降のバージョンの Windows のサインインとリリース用のドライバードライバーの種類に基づくに従います。

**注**  コード署名ポリシーを Windows である必要があります、符号付き[カタログ ファイル](catalog-files.md)システム コンポーネントおよびドライバー データベースでドライバーをインストールします。 PnP デバイスのインストールは、ドライバー データベースでの PnP ドライバー カタログ ファイルを自動的にインストールされます。 ただし、非 PnP ドライバーに署名する署名済みカタログ ファイルを使用する場合、インストール アプリケーション、ドライバーをインストールする必要がありますもファイルをインストール カタログ ドライバー データベース。

 

### <a href="" id="pnp-kernel-mode-boot-start-driver"></a> PnP カーネル モードのブート開始ドライバー

署名ポリシー ファイルを次のように、カーネル モード コードの遵守。

1.  [ドライバー ファイルをリリース署名](release-signing-a-driver-file.md)で、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)します。

2.  [ドライバー ファイルの SPC 署名を検証](verifying-the-signature-of-a-release-signed-driver-file.md)です。

内のシグネチャを埋め込み、Windows Vista 以降、*ブート開始ドライバー*ファイルは Windows の 32 ビット バージョンの省略可能です。 Windows では、カーネル モード ドライバーのファイルに埋め込みの署名があるかどうかを確認、埋め込みの署名は必要はありません。

準拠する、 [PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)の Windows Vista および Windows の以降のバージョンでは、署名する必要があります取得[カタログ ファイル](catalog-files.md)のカタログ ファイルの署名、または、 [ドライバー パッケージ](driver-packages.md)します。 ドライバー ファイルを埋め込みの署名を含めることも場合、ドライバー パッケージのカタログ ファイルを署名する前に、ドライバー ファイルに署名を埋め込みます。

場合、[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)がドライバーのプログラムで、取得、テスト、 [WHQL リリース署名](whql-release-signature.md)ドライバー パッケージ。 HCK には、ドライバーのテスト プログラムがない場合[カタログ ファイルを作成](creating-a-catalog-file-for-a-pnp-driver-package.md)し、署名、[カタログ ファイル](catalog-files.md)次のように。

**64 ビット バージョンのカタログ ファイルへの署名**

64 ビット オペレーティング システムのカタログ ファイルは、次のように署名できます。

1.  [SPC のカタログ ファイルの署名](signing-a-catalog-file-with-an-spc.md)ドライバー ファイルの署名の埋め込みに使用されました。

2.  [カタログ ファイルの SPC 署名を検証](verifying-the-spc-signature-of-a-catalog-file.md)です。 カタログ ファイルの署名を検証できるまたはカタログ ファイル内の個々 のファイルのエントリの署名を検証することができます。

**32 ビット バージョンのカタログ ファイルへの署名**

署名することができます、[カタログ ファイル](catalog-files.md)SPC をまたは 64 ビット バージョンでは、セクションで説明したように、[コマーシャル リリースの証明書](commercial-release-certificate.md)次のように。

1.  [製品版の証明書でカタログ ファイルの署名](signing-a-catalog-file-with-a-commercial-release-certificate.md)します。

2.  [カタログ ファイルの署名を検証](verifying-the-signature-of-a-catalog-file-signed-by-a-commercial-relea.md)です。 カタログ ファイルの署名を検証できるまたはカタログ ファイル内の個々 のファイルのエントリの署名を検証することができます。

### <a href="" id="non-pnp-kernel-mode-boot-start-driver"></a> 非 PnP のカーネル モードのブート開始ドライバー

に準拠して、カーネル モード コードを 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのポリシーを署名で署名を埋め込みます、*ブート開始ドライバー*ファイルの次のようにします。

1.  [ドライバー ファイルをリリース署名](release-signing-a-driver-file.md)SPC を使用します。

2.  [ドライバー ファイルの SPC 署名を検証](verifying-the-signature-of-a-release-signed-driver-file.md)です。

内のシグネチャを埋め込み、Windows Vista 以降、*ブート開始ドライバー*ファイルは Windows の 32 ビット バージョンの省略可能です。 Windows では、カーネル モード ドライバーのファイルに埋め込みの署名があるかどうかを確認、埋め込みの署名は必要はありません。

PnP デバイス インストールの署名の要件は、非 PnP ドライバーには適用されません。

### <a href="" id="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> ブート開始ドライバーではない PnP のカーネル モード ドライバー

カーネル モード コードを 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのポリシーを署名では、非ブート PnP ドライバーが埋め込みの署名がある必要はありません。 ただし、ドライバー ファイル、埋め込みの署名を含む場合、シグネチャ ファイルに埋め込まれるドライバー署名の前に、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)します。

PnP デバイス インストールの署名要件を遵守するには、署名済みカタログ ファイルを取得するか、ドライバー パッケージのカタログ ファイルに署名する必要があります。

ハードウェア認定キット (HCK) 場合。

### <a href="" id="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> ブート開始ドライバーではない非 PnP のカーネル モード ドライバー

署名の 64 ビット バージョンの Windows Vista のポリシーと以降のバージョンの Windows カーネル モード コードの遵守、ドライバー ファイルの署名を埋め込むまたはのカタログ ファイルの署名、[ドライバー パッケージ](driver-packages.md)します。

以降 Windows Vista では、ドライバー ファイルの署名の埋め込みは、Windows の 32 ビット バージョンの省略可能です。 Windows では、カーネル モード ドライバーのファイルに埋め込みの署名があるかどうかを確認、埋め込みの署名は必要はありません。

PnP デバイス インストールの署名の要件は、非 PnP ドライバーには適用されません。

**注**  署名済みカタログ ファイルを使用して通常より簡単かつよりも効率的には埋め込み署名を使用します。 詳細については、長所と短所の埋め込み署名を使用して、署名済みカタログ ファイルとは、次を参照してください。[テスト署名ドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/signing-a-driver)します。

 

ファイルでない非 PnP のカーネル モード ドライバー用にリリース署名を埋め込むには、*ブート開始ドライバー*、これらの手順に従います。

1.  [ドライバー ファイルの署名](release-signing-a-driver-file.md)SPC を使用します。

2.  [ドライバー ファイルの署名を検証](verifying-the-signature-of-a-release-signed-driver-file.md)です。

リリース記号でない非 PnP のカーネル モード ドライバー用のカタログ ファイルを*ブート開始ドライバー*、これらの手順に従います。

1.  [非 PnP ドライバーのカタログ ファイルを作成](creating-a-catalog-file-for-a-non-pnp-driver-package.md)です。

2.  [SPC のカタログ ファイルの署名](signing-a-catalog-file-with-an-spc.md)します。

3.  [カタログ ファイルの SPC 署名を検証](verifying-the-spc-signature-of-a-catalog-file.md)です。

この種類のドライバーが署名付き[カタログ ファイル](catalog-files.md)埋め込みの署名ではなく、ドライバーをインストールするインストール アプリケーションは、システム コンポーネントおよびドライバー データベースでカタログ ファイルをインストールする必要があります。 詳細については、次を参照してください。 [Release-Signed カタログ ファイルを非 PnP ドライバーのインストール](installing-a-release-signed-catalog-file-for-a-non-pnp-driver.md)します。

 

 





