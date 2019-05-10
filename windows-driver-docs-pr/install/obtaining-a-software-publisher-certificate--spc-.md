---
title: ソフトウェア発行元証明書 (SPC) の取得
description: ソフトウェア発行元証明書 (SPC) の取得
ms.assetid: 50546234-e98d-40ed-b9c6-7d78cf0419ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ade47f521f61fa7f0d31afac83c52df7c9d3854
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106437"
---
# <a name="obtaining-a-software-publisher-certificate-spc"></a>ソフトウェア発行元証明書 (SPC) の取得


リリース署名が必要です。

-   ソフトウェア発行元証明書 (SPC)、証明書の公開および秘密暗号化キーと共にします。

-   関連付けられているクロス証明書。

SPC は、商用証明書機関 (CA) から取得されます。 CA は証明書のプライベートおよびパブリック キーを提供してもします。 デジタル署名を作成するために使用する、ために、SPC とキーを Personal Information Exchange に変換する必要があります (*.pfx*) ファイル。 このプロセスの詳細については、次を参照してください。 [Personal Information Exchange (.pfx) ファイル](personal-information-exchange---pfx--files.md)します。

SPC やキーを格納すると、 *.pfx*ファイル、する必要があるない署名のコンピューター上の個人証明書ストアにインポートします。 詳細については、次を参照してください。 [SPC を証明書ストアにインポート](importing-an-spc-into-a-certificate-store.md)します。

Microsoft では、1 つクロス証明書キーのパブリック ルート証明書ごとに、カーネル モード コード署名のソフトウェア発行元の証明書の使用をサポートする ca が発行されました。 ドライバー パッケージのリリース-サインイン時に、正しいクロス証明書を使用する必要があります。 どのクロス証明書が必要なリリース署名を確認するのを参照してください。 [SPC をクロス証明書を決定する](determining-an-spc-s-cross-certificate.md)します。

SPCs を提供する証明機関の一覧については、およびクロス証明書の詳細については、「[カーネル モード コード署名用クロス証明書](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)します。 取得するための CA の web サイトの指示に従って、SPC をインストールして、対応するクロス証明書署名のコンピューターにします。

SPCs とその管理の詳細については、次を参照してください。[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)します。

 

 





