---
title: 商用リリース証明書
description: 商用リリース証明書
ms.assetid: bc3966e6-a7e4-4c5c-8dcf-9b95e61ba9b1
keywords:
- 商用リリース証明書 WDK
- カタログファイル WDK ドライバー署名、商用リリース証明書
- パブリックリリースドライバー署名 WDK、商用リリース証明書
- リリース署名 WDK、商用リリース証明書
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ed4b6ba417e892ea6604014b05a15baa51de97a
ms.sourcegitcommit: 55171d00a4d0776ffbea40ab421f765c5432fcaa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995438"
---
# <a name="commercial-release-certificate"></a>商用リリース証明書

 > [!CAUTION] 
 > 2021以降では、クロス証明書の大半が期限切れになります。 これらのクロス証明書が期限切れになると、これらのクロス証明書にチェーンされているコード署名証明書は、新しいカーネルモードデジタル署名を作成できなくなります。 これは、すべてのバージョンの Windows に影響します。 詳細については、「[ソフトウェア発行元証明書と商用リリース証明書の廃止](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)」を参照してください。
 
*商用リリース証明書*は、発行元が Microsoft ルート証明書プログラムのメンバーである信頼されたサードパーティの商用証明機関 (CA) から取得したデジタル証明書を指します。 GTE と VeriSign, Inc. は、このような Ca の2つの例です。 このプログラムのメンバーである CA は、申請者の身元と権利を検証してから、申請者がドライバの署名に使用する証明書を発行します。 署名プロセスでは、発行元の id を使用してドライバーをスタンプし、署名後にドライバーが変更されていないことを確認するために使用できます。

セキュリティ上の理由から、ドライバーのテストに署名するために使用されるデジタル証明書を使用しないようにしてください。 リリース署名とテスト署名に使用する別のデジタル証明書を取得する必要があります。 デジタル証明書の管理方法の詳細については、「[デジタル署名キーまたはコード署名キーの管理](managing-the-digital-signature-or-code-signing-keys.md)」を参照してください。

CA によって提供される指示に従って、ドライバーの署名に使用するコンピューターにリリース証明書を取得してインストールする方法について説明します。

CA からデジタル証明書を取得する方法の詳細については、 [Microsoft ルート証明書プログラムのメンバー](https://go.microsoft.com/fwlink/p/?linkid=74266)に関する web サイトを参照してください。

 

 





