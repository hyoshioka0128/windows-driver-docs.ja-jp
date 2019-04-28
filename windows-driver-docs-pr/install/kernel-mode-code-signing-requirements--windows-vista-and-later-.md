---
title: カーネル モードのコード署名の要件
description: カーネル モードのコード署名の要件
ms.assetid: da02fcb3-d073-42cd-8247-71e2e9e93f65
keywords:
- ドライバーの署名の WDK、カーネル モード コード署名の要件
- ドライバー WDK、カーネル モード コード署名の要件への署名
- デジタル署名 WDK、カーネル モード コード署名の要件
- 署名 WDK、カーネル モード コード署名の要件
- カーネル モード コード署名の WDK の要件
- カーネル モード ドライバーの WDK の署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 442d37abc86ca0b8936032b859602b9da69175e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364957"
---
# <a name="kernel-mode-code-signing-requirements"></a>カーネル モードのコード署名の要件


Windows Vista では、カーネル モード コード署名では、カーネル モード ドライバーが読み込まれるかどうかをポリシー コントロールを開始しています。 署名の要件は、Windows オペレーティング システムのバージョンとかどうか、ドライバーは署名されているパブリック リリース用または開発チームによって開発およびドライバーのテスト中に によって異なります。 [署名の要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)PnP デバイスとドライバーのインストールに関連します。

仮想ドライバーでは、実際のハードウェア ドライバーと同じ要件があります。 つまり、ターゲットが OS のバージョンの要件に準拠する必要があります。

署名とダッシュ ボードの送信については、次を参照してください。[複数の Windows バージョンの Microsoft によって署名されたドライバーを入手](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-drivers-signed-by-microsoft-for-multiple-windows-versions)します。

### <a href="" id="kernel-mode-code-signing-requirements-for-public-release-of-a-driver"></a> カーネル モード コード署名のドライバーのリリースを公開するための要件

> [!NOTE]
> 以降では、Windows 10 version 1607 では、Windows は読み込まれませんを介して Microsoft によって署名されていないが新しいカーネル モード ドライバー、[ハードウェア デベロッパー センター](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)します。  いずれかで有効な署名を取得できる[ハードウェア認定](https://docs.microsoft.com/windows-hardware/drivers/dashboard/hardware-certification-submissions)または[構成証明](https://docs.microsoft.com/windows-hardware/drivers/dashboard/attestation-signing-a-kernel-driver-for-public-release)します。 


<a href="" id="--------64-bit-versions-of-windows-starting-with-"></a> **Windows Vista と共に登場した Windows の 64 ビット バージョン**  
カーネル モード コード署名ポリシーでは、次のように、カーネル モード ドライバーに署名する必要があります。

-   カーネル モードのブート開始ドライバーが埋め込みあります[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)署名します。 これは、任意の種類のブート開始ドライバーの PnP または非 PnP カーネル モードに適用されます。

-   ブート開始ドライバーではない非 PnP のカーネル モード ドライバーには、いずれかが必要、[カタログ ファイル](catalog-files.md)SPC を署名またはドライバー ファイル含める必要があります、埋め込み SPC 署名します。

-   ブート開始ドライバーではない PnP カーネル モード ドライバー署名が必要か、埋め込み SPC、カタログのファイル、 [WHQL リリース署名](whql-release-signature.md)、または SPC シグネチャを持つカタログ ファイル。 カーネル モード コード署名ポリシーでは、PnP ドライバーのカタログ ファイルに署名する必要はありません、PnP デバイスのインストールは、ドライバーのカタログ ファイルは署名も場合にのみを符号付きとしてドライバーを扱います。

<a href="" id="32-bit-versions-of-windows"></a>**Windows の 32 ビット バージョン**  
Windows Vista および Windows の以降のバージョンは、次のドライバーに対してだけ、カーネル モード ドライバーの署名ポリシーを適用します。

-   保護されたメディアをストリームするドライバー。 これらの要件の詳細については、次を参照してください[(Windows Vista 以降) の保護されているメディア コンポーネントのコード署名。](https://go.microsoft.com/fwlink/p/?linkid=69258)

-   カーネル モード*ブート開始ドライバー*します。

### <a href="" id="kernel-mode-code-signing-requirements-during-development-and-test"></a> カーネル モード コードを開発およびテスト中に署名の要件

<a href="" id="--------64-bit-versions-of-windows-starting-with-"></a> **Windows Vista と共に登場した Windows の 64 ビット バージョン**  
カーネル モード コード署名ポリシーでは、カーネル モード ドライバーがある必要があります[テスト署名された](test-signing-driver-packages.md)がそのテスト署名と[有効になっている](the-testsigning-boot-configuration-option.md)します。 テスト署名を指定できます、 [WHQL テスト署名](whql-test-signature-program.md)によって社内で生成されたか、[テスト証明書](test-certificates.md)します。 ドライバーは、テスト署名されたようあります。

-   カーネル モード*ブート開始ドライバー*埋め込まれたテスト署名が必要です。 これは、非 PnP、PnP またはカーネル モード ドライバーの任意の型に適用されます。

-   カーネル モード ドライバーでない、*ブート開始ドライバー*いずれかをテスト署名されている必要があります[カタログ ファイル](catalog-files.md)またはドライバ ファイルは、埋め込まれたテスト署名を含める必要があります。 これは、非 PnP、PnP またはカーネル モード ドライバーの任意の型に適用されます。

<a href="" id="32-bit-versions-of-windows"></a>**Windows の 32 ビット バージョン**  
Windows Vista および Windows の以降のバージョンは、次のドライバーに対してだけ、カーネル モード ドライバーの署名ポリシーを適用します。

-   保護されたメディアをストリームするドライバー。 これらの要件の詳細については、次を参照してください[(Windows Vista 以降) の保護されているメディア コンポーネントのコード署名。](https://go.microsoft.com/fwlink/p/?linkid=69258)

-   カーネル モード*ブート開始ドライバー*します。

 

 





