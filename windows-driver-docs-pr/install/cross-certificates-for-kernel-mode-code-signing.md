---
title: カーネル モードのコード署名のクロス証明書
description: この情報では、Microsoft Windows のコード署名カーネルモードバイナリファイルのクロス証明書を取得して使用する方法について説明します。
ms.assetid: 0A1364BF-04DA-4F1C-803A-18FE2A5EF390
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2536d56a8f9f7b1ee7bc67944366f5933e72a7ff
ms.sourcegitcommit: fe3c8b53a94c35b564b04adc0d56852879a2f119
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85200197"
---
# <a name="cross-certificates-for-kernel-mode-code-signing"></a>カーネル モードのコード署名のクロス証明書


この情報では、Microsoft Windows のコード署名カーネルモードバイナリファイルのクロス証明書を取得して使用する方法について説明します。

> [!NOTE]
> Microsoft セキュリティアドバイザリ ([2880823](https://docs.microsoft.com/security-updates/SecurityAdvisories/2016/2880823)) 「Microsoft ルート証明書プログラムの sha-1 ハッシュアルゴリズムの廃止」を参照してください。このポリシーの変更については、microsoft がルート証明機関に対して x.509 ハッシュアルゴリズムを使用して、SSL とコード署名を2016年1月1日より後に実行することを許可しなくなります。

> [!NOTE]
> [Microsoft の信頼されたルートプログラム](https://docs.microsoft.com/security/trusted-root/program-requirements)は、カーネルモード署名機能を持つルート証明書をサポートしなくなりました。 詳細については、「[ソフトウェア発行元証明書の廃止、商用リリース証明書、および商用テスト証明書](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)」を参照してください。

## <a name="cross-certificates-overview"></a>クロス証明書の概要


クロス証明書は、ある証明機関 (CA) によって発行されたデジタル証明書であり、別の証明機関のルート証明書の公開キーに署名するために使用されます。 クロス証明書は、単一の信頼されたルート CA から他の複数の Ca への信頼チェーンを作成するための手段を提供します。

Windows では、クロス証明書:

-   オペレーティングシステムのカーネルに、信頼された1つの Microsoft ルート機関を与えることを許可します。
-   ソフトウェア発行元証明書 (SPCs) を発行する複数の商用 Ca に信頼チェーンを拡張します。これは、Windows での配布、インストール、および読み込みのためにコード署名ソフトウェアに使用されます。

ここで提供されているクロス証明書は、カーネルモードソフトウェアに適切に署名するための Windows Driver Kit (WDK) コード署名ツールと共に使用されます。 カーネルモードソフトウェアのデジタル署名は、Windows 向けに発行されたソフトウェアのコード署名に似ています。 クロス証明書は、カーネルモードソフトウェアに署名するときに、開発者またはソフトウェア発行者によってデジタル署名に追加されます。 クロス証明書自体は、バイナリファイルまたはカタログのデジタル署名にコード署名ツールによって追加されます。

クロス証明書を使用してサードパーティの暗号化サービスプロバイダー (Csp) に署名する方法の詳細については、[サードパーティの csp の Authenticode 署名](authenticode-signing-of-csps.md)に関する説明を参照してください。

## <a name="selecting-the-correct-cross-certificate"></a>正しいクロス証明書を選択しています


Microsoft では、コード署名カーネルモードコード用に SPCs を発行する CA ごとに、特定のクロス証明書を提供しています。 次の一覧には、SPC を発行したルート機関の正しいクロス証明書へのリンクがあります。

次の手順に従って CA を識別し、関連するクロス証明書をダウンロードします。

1.  Microsoft 管理コンソール (MMC) を開き、証明書スナップインを追加します。
    1.  [スタート] ボタンをクリックし、検索ボックスに「mmc」と入力して、return キーを押します。 [ユーザー アカウント制御] ダイアログ ボックスが表示された場合は、[はい] をクリックします。
    2.  MMC の [ファイル] メニューで、[スナップインの追加と削除] を選択します。
    3.  証明書スナップインを選択し、[追加] をクリックします。
    4.  [ユーザーアカウント] を選択し、[完了] をクリックします。
    5.  証明書スナップインをもう一度選択し、[追加] をクリックします。
    6.  [コンピューターアカウント] を選択し、[次へ] をクリックします。
    7.  [ローカルコンピューター] を選択し、[完了] をクリックします。

2.  証明書ストアで SPC を見つけて、ダブルクリックします。 証明書は、証明書のインストール方法に応じて、次の2つの場所のいずれかに一覧表示されます。
    -   現在のユーザー、個人用、証明書ストア、または
    -   ローカルコンピューターの個人用証明書ストア

3.  [**証明書**] ダイアログボックスで、[**証明のパス**] タブをクリックし、証明のパスで一番上の証明書を選択します。 これは、SPC の発行元のルート証明機関である CA です。
4.  ルート証明機関の証明書を表示するには、[**証明書の表示**] ボタンをクリックし、[新しい**証明書**] ダイアログボックスの [**詳細**] タブをクリックします。
5.  この証明書の**発行者**と**拇印**を検索します。 次に、この CA の対応するエントリを下の一覧で見つけます。
6.  カーネルモードコードにデジタル署名するときに、CA の関連するクロス証明書をダウンロードし、このクロス証明書を SPC と共に使用します。

## <a name="cross-certificate-list"></a>クロス証明書の一覧


次の一覧には、コード署名カーネルモードコードのために SPCs を発行するために Microsoft によって現在サポートされているすべての Ca が含まれています。

|                              CA                              |                 ルート証明書の拇印                 |                        ダウンロード リンク                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| Certum 信頼されたネットワーク CA                                    | 55 43 55 15 fd d2 48 65 75 fd c5 cf 3b ad 00 c9 13 12 3d 03 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321770) |
| DigiCert の保証 ID ルート CA                                  | ba 3e a5 4d 72 c1 45 d3 7c 25 5e 1e a4 0a fb c6 33 48 b9 6e | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321771) |
| DigiCert Global Root CA                                      | c9 83 39 19 f1 f3 6a 63 48 11 1e 93 02 6f d4 0e b9 6f bc 34 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321772) |
| DigiCert High Assurance EV Root CA                           | 2f 25 13 af 39 92 db 0a 3f 79 70 9f f8 14 3b 3f 7b d2 d1 43 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321773) |
| Entrust.net Certification Authority (2048)                   | 00 a3 e6 00 9e aa 73 9b 3d ee f4 b5 06 64 9e 8a 1a 7a d3 3a | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321774) |
| Entrust ルート証明機関– G2                    | d8 fc 24 87 48 58 5e 17 3e fb fb 30 75 c4 b4 d6 0f 9d 8d 08 | [ダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=624811) |
| GeoTrust Primary Certification Authority                     | e8 6e 80 82 99 0e 3d fa ed 81 6d 9e b1 72 0f 91 a4 f1 a1 85 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321775) |
| GeoTrust プライマリ証明機関– G3                | b2 bb bd fa c8 f1 a8 ad 58 95 cd 49 38 4b 22 ca 19 db 2d 1f | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321776) |
| GlobalSign Root CA                                           | cc 1d ee bf 6d 55 c2 c9 06 1b a1 6f 10 a0 bf a6 97 9a-z 4a 32 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321777) |
| ゴー Daddy ルート証明機関– G2                     | 84 2c 5c b3 4b 73 bb c5 ed 85 64 bd ed a7 86 96 7d 7b 42 ef | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321778) |
| NetLock Arany (クラス Gold)                                   | 89 4f 1d 28 97 aa 4c 07 4d cd 85 c5 fc 09 ee 73 b9 51 04 d8 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321779) |
| NetLock Platina (クラスプラチナ)                             | 97 dd 74 97 16 20 57 29 41 dc 80 0c 2f d8 0a 48 07 7d 10 b0 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321780) |
| セキュリティ通信 RootCA1                               | 41 f2 8c e5 6f d8 b9 cb 46 7f b5 03 2a 3c ae 1c dc 9d 86 48 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321781) |
| Starfield.html ルート証明機関– G2                    | 40 c2 0a 9a-z 33 fa d0 36 ac bf e8 2d 6c bb ee 1b 42 9b 86 de | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321782) |
| StartCom 証明機関                             | e6 06 9e 04 8d ea 8d 81 7a fc 41 88 b1 be f1 d8 88 d0 af 17 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321783) |
| TC TrustCenter Class 2 CA II                                 | 42 62 ff 7d 89 70 66 aa e7 75 80 d3 3a d2 88 03 f9 a1 1a 62 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321784) |
| Thawte Primary Root CA                                       | 55 38 e9 fe c1 40 30 b7 40 15 23 49 e1 15 a1 16 5d 29 07 4a | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321785) |
| Thawte プライマリルート CA – G3                                  | ba 57 ca 5e 78 dd 2d 1d 74 76 ae be e9 95 3e 39 6f d0 55 46 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321786) |
| VeriSign クラス3パブリックプライマリ証明機関– G5 | 57 53 4c cc 33 91 4c 41 f7 0e 2c bb 21 03 a1 db 18 81 7d 8b | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321787) |
| VeriSign Universal Root Certification Authority              | 9e d8 cd 56 01 f0 10 56 51 eb bb 3f 57 f0 31 82 e5 fa 7e 01 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321788) |

## <a name="new-cross-certificate-list"></a>新しいクロス証明書の一覧


次の一覧には、コード署名カーネルモードコード用に SPCs を発行するために Microsoft によって現在サポートされている新しい Ca がいくつか含まれています。


|                              CA                              |                 ルート証明書の拇印                 |                        ダウンロード リンク                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| AddTrust External CA Root                                    | a7 5a c6 57 aa 7a 4c df e5 f9 de 39 3e 69 ef ca b6 59 d2 50 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321790) |
| GoDaddy クラス2証明機関                      | d9 61 24 72 ef 0f 27 87 e2 b2 d9 e0 63 a0 6b 32 fa 5e 33 3d | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321791) |
| Starfield.html クラス2証明機関                    | f8 fc 7f 3c dd 51 76 ad d2 7c f9 7f 73 96 59 09 46 6d 9a-z 22 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321792) |
| UTN-USERFirst-Object                                         | ae 1e 25 26 01 30 a3 0b 1b c2 20 29 35 65 3b e5 a7 23 be f5 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321793) |
 

 





