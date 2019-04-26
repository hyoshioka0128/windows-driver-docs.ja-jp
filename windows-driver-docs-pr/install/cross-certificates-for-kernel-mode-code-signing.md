---
title: カーネル モードのコード署名のクロス証明書
description: この情報は、取得してコード署名用クロス証明書を使用する方法を説明します。 Microsoft Windows のカーネル モード バイナリ ファイル。
ms.assetid: 0A1364BF-04DA-4F1C-803A-18FE2A5EF390
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb5ac51943c3744b322a2c82ca6744d57bbc6f2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352079"
---
# <a name="cross-certificates-for-kernel-mode-code-signing"></a>カーネル モードのコード署名のクロス証明書


この情報は、取得してコード署名用クロス証明書を使用する方法を説明します。 Microsoft Windows のカーネル モード バイナリ ファイル。

**注**  もご覧くださいマイクロソフト セキュリティ アドバイザリ ([2880823](https://technet.microsoft.com/library/security/2880823))"非推奨の sha-1 ハッシュ アルゴリズムの Microsoft Root Certificate Program"、Microsoft のポリシーの変更を記述します。ルートの SSL とコード署名の 2016 年 1 月 1 日の後の目的の sha-1 ハッシュ アルゴリズムを使用して X.509 証明書を発行する証明書機関を許可しなくなります。

 

## <a name="cross-certificates-overview"></a>クロス証明書の概要


クロス証明書は、1 つ証明書機関 (CA) によって別の証明書機関のルート証明書の公開キーの署名に使用される発行されたデジタル証明書です。 クロス証明書は、1 つの信頼されたルート CA から他の複数の Ca への信頼チェーンを作成するための手段を提供します。

で Windows、クロス証明書。

-   1 つの信頼された Microsoft root 権限を持つオペレーティング システムのカーネルを使用できます。
-   ソフトウェア発行元証明書を発行 (SPCs)、コード署名に使用される複数の商用 Ca を信頼チェーンを拡張するソフトウェアの配布、インストール、および Windows での読み込み

ここではクロス証明書は、カーネル モードのソフトウェアを適切に署名するために、Windows Driver Kit (WDK) のコード署名ツールで使用されます。 カーネル モードのソフトウェアにデジタル署名は、Windows 用にパブリッシュされているすべてのソフトウェアのコード署名に似ています。 クロス証明書は、カーネル モードのソフトウェアのサインイン時に、開発者またはソフトウェアの発行元によってデジタル署名に追加されます。 バイナリ ファイルまたはカタログのデジタル署名をコード署名ツールで、クロス証明書自体が追加されます。

参照してください[サード パーティ製の Csp の Authenticode 署名](authenticode-signing-of-csps.md)クロス証明書を使用して、サード パーティ製の暗号化サービス プロバイダー (Csp) に署名する方法の詳細について。

## <a name="selecting-the-correct-cross-certificate"></a>適切なクロス証明書を選択します。


Microsoft では、カーネル モード コードのコード署名の SPCs を発行する各 CA に対して特定の間の証明書を提供します。 以下の一覧には、正しい間の証明書に、SPC を発行したルート証明機関のリンクがあります。

CA を識別するために次の手順に従ってし、し、関連するクロス証明書をダウンロードします。

1.  Microsoft 管理コンソール (MMC) を開き、証明書スナップインを追加します。
    1.  [スタート] ボタンをクリックして、検索ボックスに「mmc」を入力および return キーを押します。 ユーザー アカウント制御 ダイアログ ボックスが表示されている場合は、はい をクリックします。
    2.  MMC ファイル メニューで、スナップインの追加と削除を選択してください.
    3.  証明書スナップインで選択し、[追加] をクリックします。
    4.  ユーザー アカウントを選択し、完了 をクリックします。
    5.  証明書スナップインを再度選択し、[追加] をクリックします。
    6.  コンピューター アカウントを選択し、[次へ] をクリックします。
    7.  ローカル コンピューターを選択し、[完了] をクリックします。

2.  証明書ストアに、SPC を見つけて、それをダブルクリックします。 証明書のインストール方法に応じて、次の 2 つ場所のいずれかで、証明書が表示されます。
    -   現在のユーザー、個人情報、証明書ストア、または
    -   ローカル コンピューター個人証明書ストア

3.  **証明書**ダイアログ ボックスをクリックして、**証明のパス**タブ、および証明書パスには、最上位の証明書を選択します。 これは、発行元のルート機関、SPC 用の CA です。
4.  クリックして、ルート機関の証明書を表示、**証明書の表示**ボタンをクリックし、をクリックし、**詳細**の新しいタブ**証明書** ダイアログ ボックス。
5.  検索、**発行者**と**拇印**この証明書。 下の一覧で、この CA の対応するエントリを見つけます。
6.  CA の間の関連する証明をダウンロードし、カーネル モード コードにデジタル署名するときに、このクロス証明書と共に、SPC を使用

## <a name="cross-certificate-list"></a>クロス証明書の一覧


次の一覧には、カーネル モード コードのコード署名の SPCs を発行するため、Microsoft で現在サポートされている証明機関のすべてが含まれます。

|                              CA                              |                 ルート証明書の拇印                 |                        ダウンロード リンク                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| Certum には、ネットワーク CA が信頼されています。                                    | 55 43 55 15 fd d2 48 65 75 fd c5 cf 3b ad 00 c9 13 12 3d 03 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321770) |
| DigiCert は、ルート CA の ID を保証                                  | ba 3e a5 4d 72 c1 45 d3 7c 25 5e 1e a4 0a fb c6 33 48 b9 6e | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321771) |
| DigiCert グローバル ルート CA                                      | c9 83 39 19 f1 f3 6a 63 48 11 1e 93 02 6f d4 0 e b9 6f bc 34 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321772) |
| DigiCert 高保証 EV ルート CA                           | 2f 25 13 af 39 92 db 0a 3f 79 70 9f f8 14 3b 3 f 7b d2 d1 43 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321773) |
| Entrust.net 証明機関 (2048)                   | 00 a3 e6 9e 00 aa 73 9b 3d ee f4 b5 06 64 9 d 8a 1a 7a d3 3a | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321774) |
| ルート証明機関 – G2 を entrust します。                    | d8 fc 24 87 48 58 5e 17 3e fb fb 30 75 c4 b4 d6 0f 9 d 8 d 08 | [ダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=624811) |
| GeoTrust プライマリ証明機関                     | e8 6e 80 82 99 0 e 3d fa ed 81 6 d 9e b1 72 0f 91 a4 f1 a1 85 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321775) |
| GeoTrust プライマリ証明機関: G3                | b2 bb bd fa c8 f1 a8 ad 58 95 cd 49 38 4b 22 ca 19 db 2d 1 f | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321776) |
| GlobalSign ルート CA                                           | cc 1d ee bf 6 d 55 c2 c9 06 1b a1 6f 10 a0 bf a6 97 9a 4a 32 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321777) |
| Go Daddy のルート証明機関 – G2                     | 84 2c 5c b3 4b 73 bb c5 ed 85 64 bd ed a7 86 96 7d 7b 42 ef | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321778) |
| NetLock Arany (クラス金)                                   | 89 4f 1d 28 97 aa 4c 07 4d cd 85 c5 fc 09 ee 73 b9 51 04 d8 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321779) |
| NetLock Platina (プラチナのクラス)                             | 97 dd 74 97 16 20 57 29 41 dc 80 0c 2f d8 0a 48 07 7d 10 b0 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321780) |
| Security Communication RootCA1                               | 41 f2 8c e5 6f d8 b9 cb 46 7f b5 03 2a 3c ae 1c dc 9d 86 48 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321781) |
| G2 のスター フィールドのルート証明機関:                    | 40 c2 0a 9a 33 fa d0 36 ac bf e8 2d 6c bb ee 1b 42 9b 86 de | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321782) |
| StartCom 証明機関                             | e6 06 9e 04 8 d ea 8d 81 7a fc 41 88 b1 が f1 d8 88 d0 af 17 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321783) |
| TC TrustCenter クラス 2 の CA II                                 | 42 62 ff 7d 89 70 66 aa e7 75 80 d3 3a d2 88 03 f9 a1 1a 62 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321784) |
| Thawte プライマリ ルート CA                                       | 55 38 e9 fe c1 40 30 b7 40 15 23 49 e1 15 a1 16 5d 29 07 4a | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321785) |
| Thawte プライマリ ルート CA: G3                                  | ba 57 ca 5e 78 dd 2d 1d 74 76 ae be e9 95 3e 39 6f d0 55 46 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321786) |
| VeriSign クラス 3 のパブリックのプライマリ証明機関 – G5 | 57 53 4c cc 33 91 4c 41 f7 0e 2c bb 21 03 a1 db 18 81 7d 8b | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321787) |
| VeriSign ユニバーサル ルート証明機関              | 9e d8 cd 56 01 f0 10 56 51 eb bb 3f 57 f0 31 82 e5 fa 7e 01 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321788) |

## <a name="new-cross-certificate-list"></a>新しいクロス証明書の一覧


次の一覧には、カーネル モード コードのコード署名の SPCs を発行するため、Microsoft で現在サポートされているいくつかの新しい Ca が含まれています。


|                              CA                              |                 ルート証明書の拇印                 |                        ダウンロード リンク                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| AddTrust 外部 CA のルート                                    | a7 5a c6 57 aa 7a 4c df e5 f9 de 39 3e 69 ef ca b6 59 d2 50 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321790) |
| GoDaddy クラス 2 の証明機関                      | d9 61 24 72 ef 0f 27 87 e2 b2 d9 e0 63 a0 6b 32 fa 5e 33 3d | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321791) |
| 証明機関のスター フィールド クラス 2                    | f8 fc 7f 3c dd 51 76 ad d2 7c f9 7f 73 96 59 09 46 6d 9a 22 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321792) |
| UTN から USERFirst オブジェクト                                         | ae 1e 25 26 01 30 a3 0b 1b c2 20 29 35 65 3b e5 a7 23 は、f5 キーをします。 | [ダウンロード](https://go.microsoft.com/fwlink/p/?linkid=321793) |
 

 





