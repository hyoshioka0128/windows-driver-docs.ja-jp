---
title: 証明書の市販のテスト
description: 証明書の市販のテスト
ms.assetid: cedceb0c-d39e-45e2-aa42-62cd7b8bed1c
keywords:
- 市販のテスト証明書 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e0f00c371f7a939988eb837e6423d1bb0928f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551486"
---
# <a name="commercial-test-certificate"></a>証明書の市販のテスト


A*市販のテスト証明書*Microsoft ルート証明書プログラムのメンバーである信頼できる、サード パーティ商用証明機関 (CA) から発行元を取得するデジタル証明書を参照します。 GTE および VeriSign, Inc. は、このような CA の 2 つの例を示します。

Microsoft ルート証明書プログラムのメンバーである CA では、id と、申請者の権利を検証し、申請者を使用して、ドライバーに署名する証明書を発行します。 署名プロセスでは、ルーティング オーケストレーションは、発行元の id を持つドライバーとドライバーが署名された後に変更されていないことを確認するために使用できます。

市販のテスト証明書として証明書の同じ型である、[コマーシャル リリースの証明書](commercial-release-certificate.md)します。 ただし、セキュリティ上の理由から、テスト署名ドライバーもリリース ドライバーの署名に使用されるデジタル証明書いない使用する必要があります。 リリース署名し、テスト署名のために使用する個別のデジタル証明書を取得する必要があります。 デジタル証明書を管理する方法については、次を参照してください。[デジタル署名やコード署名キーを管理する](managing-the-digital-signature-or-code-signing-keys.md)します。

ドライバーを署名を取得して、コンピューターに証明書をインストールする方法、CA によって提供された指示に従います。

CA からデジタル証明書を取得する方法の詳細については、次を参照してください。、 [Microsoft ルート証明書プログラム メンバー](https://go.microsoft.com/fwlink/p/?linkid=16356) web サイト。

 

 





