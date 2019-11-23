---
title: テスト署名の概要
description: テスト署名の概要
ms.assetid: 63d4627d-b92c-489d-accf-16cfb5ac1410
keywords:
- テスト署名ドライバーパッケージ WDK、テスト署名ドライバーパッケージについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 724b495dc8a96537cdc22b025d8f8e11678bf403
ms.sourcegitcommit: c557a56ff865b5766c871e18268637dec455aa89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72512077"
---
# <a name="introduction-to-test-signing"></a>テスト署名の概要


ドライバーは、次の理由により、開発およびテスト中に[デジタル署名](digital-signatures.md)を使用してテスト署名される必要があります。

-   インストールを容易にし、自動化します。

    ドライバーが署名されていない場合、Windows Vista 以降のバージョンの Windows の[プラグアンドプレイ (PnP) ドライバーのインストールポリシー](digital-signatures-and-pnp-device-installation--windows-vista-and-late.md)では、署名されていないドライバーのインストールをシステム管理者が手動で承認して、インストールプロセスに追加の手順を追加する必要があります。 この追加の手順は、開発者やテスト担当者の生産性に悪影響を及ぼす可能性があります。 この要件をオーバーライドすることはできません。

-   Windows Vista 以降のバージョンの windows 64 でカーネルモードドライバーを読み込むことができるようにするため。

    既定では、Windows Vista 以降のバージョンの windows の[カーネルモードコード署名64ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)では、ドライバーを読み込むためにカーネルモードドライバーが署名されている必要があります。 この要件は、ドライバーの開発やデバッグを容易にするために、一時的にオーバーライドすることができます。

-   特定の種類の次世代プレミアムコンテンツを再生するには、Windows Vista 以降のバージョンの Windows のすべてのカーネルモードコンポーネントに署名する必要があります。 さらに、保護されたメディアパス (PMP) のすべてのユーザーモードおよびカーネルモードコンポーネントは、PMP 署名ポリシーに準拠している必要があります。 PMP 署名ポリシーの詳細については、 [Windows Vista での保護されたメディアコンポーネントの](http://download.microsoft.com/download/a/f/7/af7777e5-7dcd-4800-8a0a-b18336565f5b/pmp-sign.doc)ホワイトペーパー「コード署名」を参照してください。

このような理由から、Windows Vista 以降のバージョンの Windows のドライバーは、Microsoft Authenticode を使用して作成されたデジタル証明書を使用してテスト署名する必要があります。 このようなデジタル証明書は*テスト証明書*と呼ばれ、テスト証明書を使用して生成された署名は*テスト署名*と呼ばれます。

**注**  windows Vista 以降のバージョンの windows では、開発およびテストの目的でのみテスト署名されたドライバーがサポートされています。 テスト署名は、運用目的や顧客にリリースするためには使用しないでください。

 

開発チームとテストチームは、Windows Hardware Quality Labs (WHQL) がテスト目的で PnP[ドライバーパッケージ](driver-packages.md)に署名する、 [whql test Signature プログラム](whql-test-signature-program.md)に参加できます。 また、開発チームとテストチームは、独自の社内署名プロセスを管理し、次の種類の[テスト証明書](test-certificates.md)を使用してドライバーをテストすることもできます。

-   [MakeCert テスト証明書](makecert-test-certificate.md)。 [**MakeCert**](https://docs.microsoft.com/windows-hardware/drivers/devtest/makecert)ツールによって作成されたデジタル証明書です。

-   [商用テスト証明書](commercial-test-certificate.md)。 Microsoft ルート証明書プログラムのメンバーである CA によって発行されたデジタル証明書です。

-   エンタープライズ[ca テスト証明書](enterprise-ca-test-certificate.md)。エンタープライズ ca によって展開されるデジタル証明書です。

チームがテスト証明書を作成、取得、または提供した後に、テストチームがドライバーパッケージに署名する方法については、「[テスト署名ドライバーパッケージ](test-signing-driver-packages.md)」を参照してください。

テスト署名されたドライバーパッケージをインストールする方法については、「[テスト署名済みドライバーパッケージのインストール](installing-test-signed-driver-packages.md)」を参照してください。

ドライバーの初期開発とデバッグを容易にするために、カーネルモードのコード署名要件を一時的に無効にして、署名されていないカーネルモードドライバーを読み込んでテストすることができます。 ただし、システム管理者が署名されていないドライバーのインストールを承認する必要がある PnP ドライバーのインストールポリシーを無効にすることはできません。 署名されていないドライバーをインストールする方法の詳細については、「[開発およびテスト中の署名](installing-an-unsigned-driver-during-development-and-test.md)されていないドライバーのインストール」を参照してください。

ドライバーパッケージのテストに使用する最適なツールの詳細については、「[ドライバーに署名するためのツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-signing-drivers)」を参照してください。

**注**  テスト署名ドライバーパッケージに関連する手順について理解を深めるには、「[ドライバーパッケージのテスト署名方法](how-to-test-sign-a-driver-package.md)」を参照してください。 このトピックでは、テスト署名プロセスの概要について説明します。また、Windows Driver Kit (WDK) 内の*Toastpkg*サンプル[ドライバーパッケージ](driver-packages.md)を使用して、テスト署名の例をいくつか紹介します。

 

 

 





