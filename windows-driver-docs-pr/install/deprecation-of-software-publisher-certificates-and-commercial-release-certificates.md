---
title: ソフトウェア発行元証明書、商用リリース証明書、および商用テスト証明書の廃止
description: ソフトウェア発行元証明書、商用リリース証明書、および商用テスト証明書の廃止
ms.assetid: eafa4e20-94c5-49d6-a192-2fc7c9f1e64g
keywords:
- 信頼されたルート証明機関の証明書ストア WDK
- 信頼された発行元の証明書ストア WDK
ms.date: 08/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 13d142c5826d77bc4a1be46137de3b7afaefd942
ms.sourcegitcommit: 55171d00a4d0776ffbea40ab421f765c5432fcaa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "69011928"
---
# <a name="deprecation-of-software-publisher-certificates-commercial-release-certificates-and-commercial-test-certificates"></a>ソフトウェア発行元証明書、商用リリース証明書、および商用テスト証明書の廃止

[Microsoft の信頼されたルートプログラム](https://docs.microsoft.com/security/trusted-root/program-requirements)は、カーネルモード署名機能を持つルート証明書をサポートしなくなりました。

ポリシーの要件については、「 [Windows 10 カーネルモードコード署名の要件](https://docs.microsoft.com/security/trusted-root/program-requirements#f-windows-10-kernel-mode-code-signing-kmcs-requirements)」を参照してください。

カーネルモードのコード署名機能を持つ既存の[クロス署名ルート証明書](cross-certificates-for-kernel-mode-code-signing.md)は、有効期限まで続行されます。
その結果、これらのルート証明書にチェーンバックするすべての[ソフトウェア発行元証明](software-publisher-certificate.md)書、[商用リリース証明](commercial-release-certificate.md)書、および[商用テスト証明書](commercial-test-certificate.md)も、同じスケジュールで無効になります。  ドライバーが署名されるようにするには、最初に[Windows Hardware Dev Center プログラムに登録](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)します。

## <a name="frequently-asked-questions"></a>よく寄せられる質問
* [信頼されたクロス証明書の有効期限のスケジュールはどのようなものですか?](#what-is-the-expiration-schedule-of-the-trusted-cross-certificates)
* [ドライバーのテストには、クロス署名証明書に代わるものがありますか。](#what-alternatives-to-cross-signed-certificates-are-available-for-testing-drivers)
* [既存の署名済みドライバーパッケージはどうなりますか。](#what-will-happen-to-my-existing-signed-driver-packages)
* [Microsoft に公開せずに実稼働ドライバーパッケージを実行する方法はありますか。](#is-there-a-way-to-run-production-driver-packages-without-exposing-it-to-microsoft)
* [すべての新しいバージョンのドライバーパッケージをハードウェアデベロッパーセンターに再送信する必要がありますか。](#does-every-new-production-version-of-a-driver-package-need-to-be-signed-by-microsoft)
* [2021後に、サードパーティが発行した既存の証明書を使用して、ドライバー以外のコードに署名することはできますか?](#will-we-continue-to-be-able-to-sign-non-driver-code-with-our-existing-3rd-party-issued-certificates-after-2021)
* [この EV 証明書を使用して、ハードウェアデベロッパーセンターへの送信に署名することはできますか?](#will-i-be-able-to-continue-using-my-ev-certificate-for-signing-submissions-to-hardware-dev-center)
* [署名証明書がこれらの有効期限の影響を受けるかどうかを操作方法確認します。](#how-do-i-know-if-my-signing-certificate-will-be-impacted-by-these-expirations)
* [Microsoft テスト署名を自動化して、ビルドプロセスを操作するにはどうすればよいですか。](#how-can-we-automate-microsoft-test-signing-to-work-with-our-build-processes)
* [2021以降、Microsoft は実稼働カーネルモードコード署名の唯一のプロバイダーになりますか。](#starting-in-2021-will-microsoft-be-the-sole-provider-of-production-kernel-mode-code-signatures)
* [ハードウェアデベロッパーセンターでは、Windows XP のドライバー署名が提供されていません。ドライバーを XP で実行するにはどうすればよいですか。](#hardware-dev-center-doesnt-provide-driver-signing-for-windows-xp-how-can-i-have-my-drivers-run-in-xp)

### <a name="what-is-the-expiration-schedule-of-the-trusted-cross-certificates"></a>信頼されたクロス証明書の有効期限のスケジュールはどのようなものですか?

クロス署名されたルート証明書の大部分は、次のスケジュールに従って2021で期限切れになります。

|共通名| 有効期限|
|-----------|---------------|
|VeriSign クラス3パブリックプライマリ証明機関-G5       |2/22/2021|
|thawte プライマリルート CA                                             |2/22/2021|
|GeoTrust プライマリ証明機関                           |2/22/2021|
|GeoTrust プライマリ証明機関-G3                      |2/22/2021|
|thawte プライマリルート CA-G3                                        |2/22/2021|
|VeriSign ユニバーサルルート証明機関                    |2/22/2021|
|TC TrustCenter Class 2 CA II                                       |4/11/2021|
|COMODO RSA 証明機関                                 |4/11/2021|
|UTN-USERFirst オブジェクト                                               |4/11/2021|
|DigiCert の保証 ID ルート CA                                        |4/15/2021|
|DigiCert 高保証 EV ルート CA                                 |4/15/2021|
|DigiCert グローバルルート CA                                            |4/15/2021|
|Entrust.net 証明機関 (2048)                         |4/15/2021|
|GlobalSign ルート CA                                                 |4/15/2021|
|ゴー Daddy ルート証明機関-G2                           |4/15/2021|
|Starfield.html ルート証明機関-G2                          |4/15/2021|
|NetLock Arany (クラス Gold) Fotanúsítvány                           |4/15/2021|
|NetLock Arany (クラス Gold) Fotanúsítvány                           |4/15/2021|
|NetLock Platina (クラスプラチナ) Fotanúsítvány                     |4/15/2021|
|セキュリティ通信 RootCA1                                     |4/15/2021|
|StartCom 証明機関                                   |4/15/2021|
|Certum 信頼されたネットワーク CA                                          |4/15/2021|
|COMODO ECC 証明機関                                 |4/11/2021|

### <a name="what-alternatives-to-cross-signed-certificates-are-available-for-testing-drivers"></a>ドライバーのテストには、クロス署名証明書に代わるものがありますか。

次の代替手段を使用できます。

- [MakeCert プロセス](makecert-test-certificate.md)
- [WHQL テスト署名プログラム](whql-test-signature-program.md)
- [エンタープライズ CA プロセス](enterprise-ca-test-certificate.md)

これらのオプションを使用するには、 [Testsigning](the-testsigning-boot-configuration-option.md)を有効にする必要があります。 詳細については[、「開発およびテスト中のドライバー](signing-drivers-during-development-and-test.md)への署名」を参照してください。

### <a name="what-will-happen-to-my-existing-signed-driver-packages"></a>既存の署名済みドライバーパッケージはどうなりますか。 

ドライバーパッケージが中間証明書の有効期限の前にタイムスタンプされている限り、これらのパッケージは引き続き機能します。

### <a name="is-there-a-way-to-run-production-driver-packages-without-exposing-it-to-microsoft"></a>Microsoft に公開せずに実稼働ドライバーパッケージを実行する方法はありますか。 

いいえ。すべての実稼働ドライバーパッケージは、に送信され、Microsoft によって署名される必要があります。 

### <a name="does-every-new-production-version-of-a-driver-package-need-to-be-signed-by-microsoft"></a>ドライバーパッケージの新しい製品版はすべて、Microsoft によって署名されている必要がありますか。

はい。運用レベルのドライバーパッケージを再構築するたびに、Microsoft によって署名されている必要があります。

### <a name="will-we-continue-to-be-able-to-sign-non-driver-code-with-our-existing-3rd-party-issued-certificates-after-2021"></a>2021後に、サードパーティが発行した既存の証明書を使用して、ドライバー以外のコードに署名することはできますか?

はい。これらの証明書は、有効期限が切れるまで引き続き機能します。 これらの証明書を使用して署名されたコードは、ユーザーモードでのみ実行でき、有効な Microsoft 署名がない限り、カーネルでの実行は許可されません。

### <a name="will-i-be-able-to-continue-using-my-ev-certificate-for-signing-submissions-to-hardware-dev-center"></a>この EV 証明書を使用して、ハードウェアデベロッパーセンターへの送信に署名することはできますか?  

はい、有効な EV 証明書を使用して、ハードウェアデベロッパーセンターの送信パッケージに署名することはできますが、EV 証明書によって署名されたドライバーパッケージは、証明書の有効期限後に検証されなくなりました。 

### <a name="how-do-i-know-if-my-signing-certificate-will-be-impacted-by-these-expirations"></a>署名証明書がこれらの有効期限の影響を受けるかどうかを操作方法確認します。 

クロス証明書チェーンがで`Microsoft Code Verification Root`終了した場合、署名証明書が影響を受けます。 

クロス証明書チェーンを表示するに`signtool verify /v /kp <mydriver.sys>`は、を実行します。 以下に例を示します。

![[クロス証明書チェーンの検索]](images/signtoolcrosssigexample.png)

### <a name="how-can-we-automate-microsoft-test-signing-to-work-with-our-build-processes"></a>Microsoft テスト署名を自動化して、ビルドプロセスを操作するにはどうすればよいですか。

ビルドプロセスは、[ハードウェアデベロッパーセンター API](../dashboard/dashboard-api.md)を呼び出すことができます。 

使用法を示すサンプルについては、 [Surface Dev Center Manager](https://github.com/Microsoft/SDCM)リポジトリを参照してください。

### <a name="starting-in-2021-will-microsoft-be-the-sole-provider-of-production-kernel-mode-code-signatures"></a>2021以降、Microsoft は実稼働カーネルモードコード署名の唯一のプロバイダーになりますか。 

可能。

### <a name="hardware-dev-center-doesnt-provide-driver-signing-for-windows-xp-how-can-i-have-my-drivers-run-in-xp"></a>ハードウェアデベロッパーセンターでは、Windows XP のドライバー署名が提供されていません。ドライバーを XP で実行するにはどうすればよいですか。

ドライバーは、サードパーティが発行したコード署名証明書を使用して署名することもできます。 ただし、ドライバーに署名した証明書は、ターゲットコンピューター `Local Computer Trusted Publishers`の証明書ストアにインポートする必要があります。 詳細については、[信頼された発行元の証明書ストア](trusted-publishers-certificate-store.md)を参照してください。

## <a name="related-information"></a>関連情報

* [ハードウェア プログラムの登録](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)
* [ソフトウェア発行元証明書](software-publisher-certificate.md)
* [商用リリース証明書](commercial-release-certificate.md)
* [商用テスト証明書](commercial-test-certificate.md)
