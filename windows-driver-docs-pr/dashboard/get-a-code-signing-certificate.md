---
title: コード署名証明書の取得
description: コード署名証明書の取得
ms.assetid: 6CF4111A-C645-40F5-8D45-55F46B3C0740
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aa376e34cb96f62cdab31785874caa60b5a05ee
ms.sourcegitcommit: 969a98d4866be74e145df617a9f0963053898a0d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153171"
---
# <a name="get-a-code-signing-certificate"></a>コード署名証明書の取得

パートナー センター アカウントを設定するには、デジタル情報を保護するためのコード署名証明書をあらかじめ取得しておく必要があります。 この証明書は、提出するコードに対する会社の所有権を確立するための公認されている標準です。 .exe、.cab、.dll、.ocx、.msi、.xpi、.xap ファイルなどの PE バイナリにデジタル署名できます。

## <a name="step-1-obtain-an-ev-certificate"></a>手順 1:EV 証明書を取得する

- Microsoft では、Microsoft の信頼されたルート証明書プログラムの一環として、カーネル モード コード署名に登録して承認されたパートナーからの拡張された検証 (EV) コード署名証明書を求めています。 これらの機関のいずれかからの承認された EV 証明書を既に持っている場合は、その証明書を使ってパートナー センター アカウントを設定できます。 証明書を持っていない場合は、新しい証明書を購入する必要があります。

## <a name="step-2-buy-a-new-code-signing-certificate"></a>手順 2:新しいコード署名証明書を購入する

承認された EV コード署名証明書がない場合は、次のいずれかの証明機関から証明書を購入できます。

### <a name="extended-validation-code-signing-certificates"></a>拡張検証コード署名証明書

- [SSL.com の EV コード署名証明書を購入する](https://www.ssl.com/certificates/ev-code-signing/)

- [Symantec の EV コード署名証明書を購入する](https://go.microsoft.com/fwlink/?LinkId=393248)

- [Certum の EV コード署名証明書を購入する](https://go.microsoft.com/fwlink/?linkid=843061)

- [Entrust の EV コード署名証明書を購入する](https://www.entrustdatacard.com/products/digital-signing-certificates/code-signing-certificates)

- [GlobalSign の EV コード署名証明書を購入する](https://go.microsoft.com/fwlink/p/?LinkId=620888)

- [Sectigo (旧 Comodo) の EV コード署名証明書を購入する](https://go.microsoft.com/fwlink/?linkid=863208)

- [DigiCert の EV コード署名証明書を購入する](https://go.microsoft.com/fwlink/?LinkId=393249)

  1. **[DigiCert Code Signing Certificates for Sysdevs]** (Sysdevs 用 DigiCert コード署名証明書) ページで **[開始]** をクリックします。

  2. **[DigiCert Order Form]** (DigiCert 注文フォーム) ページ (手順 1.) の **[コード署名]** セクションで、 **[EV Code Signing Certificate]** (EV コード署名証明書) をクリックします。フォームの残りの情報を入力して、 **[続行]** をクリックします。

  3. DigiCert によって提示されている証明書の購入手順に従います。

## <a name="step-3-retrieve-code-signing-certificates"></a>手順 3:コード署名証明書を取得する

証明機関によって連絡先情報が検証され、証明書の購入が承認されたら、証明機関の指示に従って証明書を取得します。

> [!NOTE]
> 証明書の取得には、同じコンピューターとブラウザーを使う必要があります。

## <a name="next-steps"></a>次の手順

- 新しいパートナー センター アカウントを設定する場合は、「[ハードウェア プログラムの登録](register-for-the-hardware-program.md)」の手順を実行します。

- パートナー センター アカウントを既に設定しており、証明書を更新する必要がある場合は、「[コード署名証明書の追加または更新](update-a-code-signing-certificate.md)」の手順を実行します。

## <a name="code-signing-faq"></a>コード署名 FAQ

ここでは、Windows 10 のコード署名についてよく寄せられる質問に対してお答えします。 その他のコード署名情報は、Windows ハードウェア認定に関するブログでご確認いただけます。

- [Windows 10 のドライバー署名の変更点に関するページ](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10/ba-p/364859)
- [Windows 10 バージョン 1607 のドライバー署名の変更点](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10-version-1607/ba-p/364894)
- [Sysdev EV 証明書要件の更新に関するページ](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Update-on-Sysdev-EV-Certificate-requirement/ba-p/364879)

### <a name="hlk-tested-and-dashboard-signed-drivers"></a>HLK テスト済みのダッシュボードで署名されたドライバー

- HLK テストに合格し、ダッシュボードで署名されたドライバーは、Windows Server エディションを含む Windows Vista から Windows 10 すべてで動作します。 これは、すべての OS バージョンで同じ処理になるため、ドライバー署名の方法として推奨されています。 また、ドライバーが HLK テスト済みであるということは、優れた Windows エクスペリエンスを提供できるように、製造元が自社のハードウェアを厳格にテストし、信頼性、セキュリティ、電力効率性、保守、およびパフォーマンスに関する Microsoft のすべての要件を満たしたことを示します。 これには、適切なインストール、展開、接続、相互運用を行えるように、業界標準に準拠していることと、テクノロジに固有の機能に関する Microsoft の仕様に準拠していることが含まれます。 HLK について詳しくは、「[Windows ハードウェアの互換性プログラム](https://docs.microsoft.com/windows-hardware/design/compatibility/index)」をご覧ください。

### <a name="windows-10-desktop-attestation-signing"></a>Windows 10 デスクトップの構成証明署名

- 構成証明署名を使ってダッシュボードで署名されたドライバーは、Windows 10 デスクトップ以降のバージョンの Windows でのみ動作します。
- 構成証明署名されたドライバーは、Windows 10 デスクトップのみで動作し、Windows 7、Windows 8.1、Windows Server 2016 などのその他のバージョンの Windows では動作しません。
- 構成証明署名は、Windows 10 デスクトップのカーネル モード ドライバーとユーザー モード ドライバーをサポートしています。

### <a name="windows-10-earlier-certificate-transition-signing"></a>Windows 10 以前での証明書移行署名

- 以下は、Windows 10 1803 以前にのみ適用されます。  Windows 10 1809 以降では、これらは動作しません。
- Windows 10 では、2015 年 7 月 29 日より後に発行されたいずれかの証明書を使って署名されたタイムスタンプ付きのドライバーは推奨されません。
- 2015 年 7 月 29 日より後に有効期限が切れるいずれかの証明書を使って署名されたタイムスタンプなしのドライバーは、証明書の有効期限が切れるまで Windows 10 で機能します。

### <a name="cross-signing-and-sha-256-certificates"></a>クロス署名と SHA-256 証明書

クロス署名では、Microsoft が信頼する証明書機関 (CA) によって発行された証明書を使ってドライバーが署名されるプロセスについて説明します。 詳しくは、[クロス証明書の概要に関するページ](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)をご覧ください。

- SHA-256 は Windows 8 以降のバージョンでサポートされます。
- 修正プログラムを適用する場合は、Windows 7 でも、SHA-256 をサポートします。 修正プログラムを適用していない Windows 7 を実行するデバイスをサポートする必要がある場合は、SHA-1 証明書を使ってクロス署名するか、署名するためにダッシュボードに提出する必要があります。 それ以外の場合は、SHA-1 または SHA-2 証明書を使ってクロス署名するか、署名用の HLK/HCK 申請を作成することができます。
- Windows Vista では SHA-256 はサポートされないため、SHA-1 証明書を使ってクロス署名するか、Windows Vista のドライバー署名用の HLK/HCK 申請を作成する必要があります。
- 2015 年 7 月 29 日より前に発行された SHA-256 証明書 (EV 証明書を含む) を使ってクロス署名されたドライバーは、Windows 8 以降で動作します。 Windows Vista または Windows Server 2008 では動作しません。
- Windows Update を通じて今年の前半に発行された更新プログラムが適用されている場合は、Windows 7 または Server 2008 R2 でも、2015 年 7 月 29 日より前に発行された SHA-256 証明書 (EV 証明書を含む) を使ってクロス署名されたドライバーが動作します。 詳しくは、「[Windows 7 および Windows Server 2008 R2 で SHA-2 ハッシュ アルゴリズムを利用可能](https://docs.microsoft.com/security-updates/SecurityAdvisories/2014/2949927)」と「[マイクロソフト セキュリティ アドバイザリ:Windows 7 および Windows Server 2008 R2 で SHA-2 コード署名サポートを利用可能(2015 年 3 月 10 日)](https://support.microsoft.com/help/3033929/microsoft-security-advisory-availability-of-sha-2-code-signing-support)」をご覧ください。
- 2015 年 7 月 29 日より前に発行された SHA-1 証明書を使ってクロス署名されたドライバーは、Windows Vista から Windows 10 までのすべてのプラットフォームで動作します。
- Windows 10 では、2015 年 7 月 29 日より後に発行された SHA-1 または SHA-256 証明書を使ってクロス署名されたドライバーは推奨されません。
- SHA-256 証明書への移行作業について詳しくは [Windows における Authenticode コード署名の強制とタイムスタンプに関するページ](https://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)をご覧ください。

### <a name="windows-defender-application-control"></a>Windows Defender アプリケーション制御

- 企業は、Windows 10 Enterprise edition を使って、ドライバーの署名要件を変更するポリシーを実装することができます。 Windows Defender Application Control (WDAC) では、企業が定義したコードの整合性ポリシーを提供します。このポリシーは、少なくとも構成証明署名されたドライバーを必要とするように構成できます。 WDAC の詳細については、「[Windows Defender Application Control のデプロイプロセスの計画と作業の開始](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)」を参照してください。

### <a name="windows-server"></a>Windows Server

- Windows Server 2016 以降では、構成証明されたデバイスおよびフィルター ドライバーの署名申請は受け入れません。
- ダッシュボードでは、HLK テストに合格したデバイスおよびフィルター ドライバーのみに署名します。
- Windows Server 2016 以降では、HLK テストに合格したダッシュボード署名済みドライバーのみを読み込みます。

### <a name="ev-certs"></a>EV 証明書

- 2015 年 10 月 31 日の時点でハードウェア デベロッパー センター ダッシュボード アカウントには、構成証明署名のためのバイナリまたは HLK 認定のためのバイナリを提出する目的で、少なくとも 1 つの EV 証明書が関連付けられている必要があります。
- 提出されたバイナリそのものが署名されている必要があります。

### <a name="os-support-summary"></a>OS のサポートの概要

次の表は、Windows のドライバー署名要件をまとめたものです。

|                                    |                                |                                    |                                                                                |
|------------------------------------|--------------------------------|------------------------------------|--------------------------------------------------------------------------------|
|                                    | *構成証明ダッシュボード署名* | *HLK テストに合格したダッシュボード署名* | *2015 年 7 月 29 日より前に発行された SHA-1 証明書を使ったクロス署名*         |
| Windows Vista                      | いいえ                             | はい                                | はい                                                                            |
| Windows 7                          | いいえ                             | はい                                | はい                                                                            |
| Windows 8 / 8.1                    | いいえ                             | はい                                | はい                                                                            |
| Windows 10                         | はい                            | はい                                | X (Windows 10 1809 以降)                                                                            |
| Windows 10 - DG 有効            | \*構成による      | \*構成による          | \*構成による                                                      |
| Windows Server 2008 R2             | いいえ                             | はい                                | はい                                                                            |
| Windows Server 2012 R2             | いいえ                             | はい                                | はい                                                                            |
| Windows Server 2016 以降             | いいえ                             | はい                                | はい                                                                            |
| Windows Server 2016 以降 – DG 有効| \*構成による      | \*構成による          | \*構成による                                                      |
| Windows IoT Enterprise             | はい                            | はい                                | はい                                                                            |
| Windows IoT Enterprise - DG 有効 | \*構成による      | \*構成による          | \*構成による                                                      |
| Windows IoT Core(1)                | 要 (必須ではない)             | 要 (必須ではない)                 | 要 (2015 年 7 月 29 日以降後に発行された証明書ではクロス署名も機能します) |

\*構成による - Windows 10 Enterprise エディションでは、組織は、カスタム ドライバーの署名要件を定義する Windows Defender Application Control (WDAC) を使えます。 WDAC の詳細については、「[Windows Defender Application Control のデプロイプロセスの計画と作業の開始](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)」を参照してください。

(1) IoT Core を使って小売製品 (開発目的ではない製品) を構築する製造元には、ドライバーの署名が必要です。 承認済みの証明機関 (CA) の一覧については、「[カーネル モードのコード署名用クロス証明書](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)」をご覧ください。 UEFI セキュア ブートが有効な場合、ドライバーは署名されている必要があります。
