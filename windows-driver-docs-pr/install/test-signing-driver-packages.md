---
title: ドライバー パッケージのテスト署名
description: ドライバー パッケージのテスト署名
ms.assetid: 84727762-5ba0-48ea-8d5a-7ac54aadbb7e
keywords:
- ドライバー WDK、ドライバー パッケージの署名
- ドライバー WDK、ドライバー パッケージの署名
- WDK、ドライバー パッケージのデジタル署名
- WDK、ドライバー パッケージの署名
- ドライバー パッケージのデジタル署名 WDK
- パッケージのデジタル署名 WDK
- テスト署名ドライバー WDK、ドライバー パッケージ
- テスト署名ドライバー パッケージ WDK
- テスト署名ドライバー パッケージ、WDK テスト署名ドライバー パッケージについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3774b4f68596745731e02b857f04f6fec270a059
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380972"
---
# <a name="test-signing-driver-packages"></a>ドライバー パッケージのテスト署名


このセクションに Windows Vista および Windows の以降のバージョンをリリース用のドライバーの署名を検査するコンピューターを参照として、*コンピューターを署名*します。 署名のコンピューターでは、Windows XP SP2 または以降のバージョンの Windows が実行されている必要があります。 たとえば、ドライバーが Windows 7 のリリースのためのものは、Windows Vista を実行するコンピューターで署名できます。

使用するには、[ドライバーの署名ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-signing-drivers)WDK の以降のバージョンがインストールされている、署名のコンピューターは、Windows Vista をいる必要があります。

**注**  のバージョンを使用する必要があります、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool) Windows Vista およびそれ以降のバージョンの Windows Driver Kit (WDK) で提供されるツールです。 以前のバージョンの SignTool の署名ポリシーを Windows Vista 以降のバージョンの Windows カーネル モード コードではできません。

 

準拠する、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)と[プラグ アンド プレイ (PnP) デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)Windows Vista 以降のバージョンの Windows の中にドライバーを署名する必要があります、開発、およびそのドライバーのテスト。 署名できますのドライバー署名のコンピューターでは、次のように、ドライバーの種類に基づきます。

**注**  コード署名ポリシーを Windows である必要があります、符号付き[カタログ ファイル](catalog-files.md)の[ドライバー パッケージ](driver-packages.md)システム コンポーネントおよびドライバー データベースにインストールします。 PnP デバイスのインストールは、ドライバー データベースでの PnP ドライバー カタログ ファイルを自動的にインストールされます。 ただし、非 PnP ドライバーに署名する署名済みカタログ ファイルを使用する場合、インストール アプリケーション、ドライバーをインストールする必要がありますもファイルをインストール カタログ ドライバー データベース。

 

### <a href="" id="pnp-kernel-mode-boot-start-driver"></a> PnP カーネル モードのブート開始ドライバー

署名ポリシー ファイルを次のように、カーネル モード コードの遵守。

1.  [テスト署名ドライバー ファイル](test-signing-a-driver-file.md)します。

2.  [テスト署名されたドライバー ファイルの署名を検証](verifying-the-signature-of-a-test-signed-driver-file.md)です。

内のシグネチャを埋め込み、Windows Vista 以降、*ブート開始ドライバー*ファイルは Windows の 32 ビット バージョンの省略可能です。 Windows は、カーネル モード ドライバー ファイルの埋め込みの署名を確認、埋め込みの署名は必要はありません。

準拠する、 [PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)の Windows Vista および Windows の以降のバージョンでは、する必要がありますもテスト署名、[カタログ ファイル](catalog-files.md)の[のドライバーパッケージ](driver-packages.md). ドライバー ファイルを埋め込みの署名を含めることも場合、ドライバー パッケージのカタログ ファイルを署名する前に、ドライバー ファイルに署名を埋め込みます。

要求を送信することができます、 [Windows Hardware Quality Labs (WHQL) テスト署名](whql-test-signature-program.md)、[カタログ ファイル](catalog-files.md)します。 または、ことができますテスト署名カタログ ファイルを自分でテスト証明書で、次のように。

1.  [カタログ ファイルを作成](creating-a-catalog-file-for-a-test-signed-driver-package.md)です。

2.  [テスト署名カタログ ファイル](test-signing-a-catalog-file.md)します。

3.  [テスト署名済みカタログ ファイルの署名を検証](verifying-the-signature-of-a-test-signed-catalog-file.md)です。

    カタログ ファイル自体の署名またはカタログ ファイルに対応するエントリがある個々 のファイルの署名を確認することができます。

### <a href="" id="non-pnp-kernel-mode-boot-start-driver"></a> 非 PnP のカーネル モードのブート開始ドライバー

に準拠して、カーネル モード コードを 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのポリシーを署名で署名を埋め込みます、*ブート開始ドライバー*ファイルの次のようにします。

1.  [テスト署名ドライバー ファイル](test-signing-a-driver-file.md)します。

2.  [テスト署名されたドライバー ファイルの署名を検証](verifying-the-signature-of-a-test-signed-driver-file.md)です。

内のシグネチャを埋め込み、Windows Vista 以降、*ブート開始ドライバー*ファイルは Windows の 32 ビット バージョンの省略可能です。 Windows は、カーネル モード ドライバー ファイルの埋め込みの署名を確認、埋め込みの署名は必要はありません。

[PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)非 PnP ドライバーには適用されません。

### <a href="" id="pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> ブート開始ドライバーではない PnP のカーネル モード ドライバー

カーネル モード コードを 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのポリシーを署名では、埋め込みのシグネチャを持つ非ブートの PnP ドライバーは必要ありません。 ただし、ドライバー ファイル、埋め込みの署名を含む場合、シグネチャ ファイルに埋め込まれるドライバー署名の前に、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)します。

ない PnP カーネル モード ドライバー用、*ブート開始ドライバー*、カーネル モードのコード署名で Windows Vista の 64 ビット バージョンと以降のバージョンの Windows では、同様のポリシーに準拠しているドライバー パッケージのカタログ ファイルへの署名PnP デバイスのインストールと Windows Vista 以降のすべてのバージョンの要件を署名します。

Windows Hardware Quality Labs (WHQL) テスト署名から要求を送信できます。

### <a href="" id="non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a> ブート開始ドライバーではない非 PnP のカーネル モード ドライバー

カーネル モード コード署名 64 ビット バージョンの Windows Vista と Windows の以降のバージョンのポリシーに準拠するには、ドライバー ファイルまたは記号に署名を埋め込む、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)します。

以降 Windows Vista では、ドライバー ファイルの署名の埋め込みは、Windows の 32 ビット バージョンの省略可能です。 Windows は、カーネル モード ドライバー ファイルの埋め込みの署名を確認、埋め込みの署名は必要はありません。

PnP デバイス インストールの署名の要件は、非 PnP ドライバーには適用されません。

**注**  一般的により簡単かつ署名済みカタログ ファイルを使用するよりも効率的には埋め込みの署名を使用します。 詳細については、長所と短所の埋め込み署名を使用して、署名済みカタログ ファイルとは、次を参照してください。[テスト署名ドライバー](https://docs.microsoft.com/windows-hardware/drivers)します。

 

### <a name="to-embed-a-test-signature-in-a-file-for-a-non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a>ブート開始ドライバーではない非 PnP のカーネル モード ドライバー用のファイルにテスト署名を埋め込むには

1.  [テスト署名ドライバー ファイル](test-signing-a-driver-file.md)します。

2.  [テスト署名されたドライバー ファイルの署名を検証](verifying-the-signature-of-a-test-signed-driver-file.md)です。

### <a name="to-test-sign-a-catalog-file-for-a-non-pnp-kernel-mode-driver-that-is-not-a-boot-start-driver"></a>テスト署名、非 PnP のカーネル モード ドライバー用のカタログ ファイルでないブート開始ドライバー

1.  [非 PnP ドライバーのカタログ ファイルを作成](creating-a-catalog-file-for-a-non-pnp-driver-package.md)です。

2.  [テスト署名カタログ ファイル](test-signing-a-catalog-file.md)します。

3.  [テスト署名済みカタログ ファイルの署名を検証](verifying-the-signature-of-a-test-signed-catalog-file.md)です。

 

 





