---
title: デジタル署名
description: デジタル署名
ms.assetid: 637212b2-bc57-414b-9a06-07f79d9264f9
keywords:
- ドライバー パッケージのデジタル署名 WDK
- パッケージのデジタル署名 WDK
- WDK、ドライバー パッケージのデジタル署名
- WDK、ドライバー パッケージの署名
- ドライバー WDK、ドライバー パッケージの署名
- ドライバー WDK、ドライバー パッケージの署名
- WDK、デジタル署名デバイスのインストール
- ドライバー WDK の署名
- デジタル署名に関する証明書、WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ef6a69e6867bc6edddd97a624d4073b1066dad1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531347"
---
# <a name="digital-signatures"></a>デジタル署名


デジタル署名は Microsoft に基づく Microsoft 公開キー基盤テクノロジに基づいて[Authenticode](authenticode.md)信頼された証明機関 (Ca) のインフラストラクチャと組み合わせて使用します。 業界標準に基づく、Authenticode、により、ベンダー、または*ソフトウェア発行者*、ファイルまたはファイルのコレクションに署名する (など、[ドライバー パッケージ](driver-packages.md)) コード署名を使用して[デジタル証明書](digital-certificates.md)CA によって発行されました。

Windows では、有効なデジタル署名を使用して、次のことを確認します。

-   ファイルまたはファイルのコレクションに署名します。

-   署名者が信頼されます。

-   署名者を認証した機関は信頼されています。

-   パブリッシュされた後、ファイルのコレクションは変更されていません。

この署名プロセスなどの[ドライバー パッケージ](driver-packages.md)次が含まれます。

-   発行元を取得、 *X.509 デジタル証明書*CA から発行します。 Authenticode 証明書として別名を*署名証明書*します。 署名証明書は、一連のデータを発行元を識別し、CA が発行元の身元を確認した後のみに、CA によって発行されます。 Microsoft CA、サード パーティの商用 CA またはエンタープライズ CA の CA ができます。

    署名証明書の署名に使用、[カタログ ファイル](catalog-files.md)ドライバー パッケージの[署名を埋め込む](embedded-signatures-in-a-driver-file.md)ドライバー ファイルにします。 信頼された発行元 ca と信頼された Ca を識別する証明書がインストールされている[証明書のストア](certificate-stores.md)Windows により管理されています。

-   署名証明書には秘密キーと呼ばれる、公開キーが含まれています、*キーのペア*します。 カタログ ファイルの署名に秘密キーが使用される、[ドライバー パッケージ](driver-packages.md)またはドライバー ファイルの署名を埋め込む。 ドライバー パッケージのカタログ ファイルの署名または署名ドライバー ファイルに埋め込まれていることを確認する公開キーが使用されます。

-   カタログ ファイルに署名または署名をファイルに埋め込むには、署名プロセス最初に、暗号化ハッシュが生成されますまたは*拇印*ファイルの。 署名のプロセスは、秘密キーを使用してファイルの拇印を暗号化し、ファイルに、拇印を追加します。

    署名プロセスでは、パブリッシャーと署名証明書を発行した CA に関する情報も追加されます。 デジタル署名は、ファイルの拇印が生成されたときに処理されていないファイルのセクションで、ファイルに追加されます。

-   ファイルのデジタル署名を確認するには、Windows は、パブリッシャーと、CA に関する情報を抽出し、暗号化されたファイルの拇印を復号化する公開キーを使用します。

    Windows では、次の条件に当てはまる場合にのみ、ファイルの整合性と、発行元の信頼性。

    -   復号化された拇印では、ファイルの拇印と一致します。
    -   発行元の証明書がインストールされている、[信頼された発行元証明書ストア](trusted-publishers-certificate-store.md)します。
    -   発行元の証明書を発行した CA のルート証明書がインストールされている、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)します。

プラグ アンド プレイ (PnP) デバイスのインストールでのデジタル署名の使用方法の詳細については、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)を参照してください[デジタル署名と PnP デバイスインストール](digital-signatures-and-pnp-device-installation.md)します。

Microsoft 公開キー基盤テクノロジ、コード署名、およびデジタル署名の詳細については、次を参照してください。[コード署名の概要](https://go.microsoft.com/fwlink/p/?linkid=104071)と[コード署名のベスト プラクティス](https://go.microsoft.com/fwlink/p/?linkid=68250)します。

 

 





