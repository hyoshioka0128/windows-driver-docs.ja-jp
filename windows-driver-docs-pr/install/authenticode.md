---
title: Authenticode デジタル署名
description: Authenticode デジタル署名
ms.assetid: b4cddf64-dc1a-47b7-803d-afb1e175c9d5
keywords:
- Authenticode WDK ドライバーの署名
- ドライバー WDK、Authenticode の署名
- ドライバー WDK、Authenticode の署名
- デジタル署名、WDK Authenticode
- WDK、Authenticode の署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40529ece337b1b32c1b3107204b933f3bb2f0eb1
ms.sourcegitcommit: ba351c01be491b8ab5c74d778ab02c8766a5667a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041375"
---
# <a name="authenticode-digital-signatures"></a>Authenticode デジタル署名


Authenticode は、Authenticode で署名されたソフトウェアの発行者を識別する Microsoft コード署名テクノロジです。 また、Authenticode は、署名および公開するために、ソフトウェアが改ざんされていないことを確認します。

Authenticode では、暗号化技術を使用して、パブリッシャーの id とコードの整合性を検証します。 記載されているパブリッシャーからドライバーの発生元のユーザーを確保するために証明機関 (Ca) を含む、信頼されたエンティティのインフラストラクチャとデジタル署名が組み合わされています。 Authenticode では、信頼されたルート証明書までのデジタル署名の証明書を連鎖させることにより、ソフトウェア パブリッシャーの id を確認することができます。

ソフトウェア パブリッシャー Authenticode を使用して、ドライバーに署名または[ドライバー パッケージ](driver-packages.md)、タグ付けすることで、[デジタル証明書](digital-certificates.md)の受信者を提示し、パブリッシャーの id を検証をコード、コードの整合性を検証することができます。 証明書は、ソフトウェア パブリッシャーを識別するデータのセットです。 そのソフトウェアの発行元の id を検証した後にのみ、CA によって発行されます。 証明書データには、発行元の公開暗号化キーが含まれています。 証明書は、通常、最終的には、VeriSign などのよく知られている CA を参照するこのような証明書のチェーンの一部です。

Authenticode コード署名では、ドライバーの実行可能ファイルの部分は変更されません。 代わりに、次は。

-   埋め込みのシグネチャを持つ署名プロセスには、ドライバー ファイルの nonexecution 部分に含まれるデジタル署名が埋め込まれます。 このプロセスの詳細については、次を参照してください。[ドライバー ファイルの埋め込み署名](embedded-signatures-in-a-driver-file.md)します。

-   デジタル署名された[カタログ ファイル](catalog-files.md)( *.cat*)、署名プロセス内の各ファイルの内容からファイルのハッシュ値を生成する必要があります、[ドライバー パッケージ](driver-packages.md)します。 カタログ ファイルでは、このハッシュ値が含まれます。 カタログ ファイルは、埋め込みの署名で署名し、されます。 この方法では、カタログ ファイルは、デタッチされた署名の種類です。

**注**  、[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)さまざまなデバイスの種類のテスト カテゴリがあります。 テスト カテゴリの一覧をご覧[HLK API リファレンス](https://docs.microsoft.com/windows-hardware/test/hlk/api/hlk-api-reference)します。 ソフトウェア パブリッシャーを取得する必要があります、デバイスの種類のテスト カテゴリがこの一覧に含まれる場合、 [WHQL リリース署名](whql-release-signature.md)の[ドライバー パッケージ](driver-packages.md)ただし、HCK がテスト プログラムを持たないかどうか、デバイスの種類、ソフトウェアの発行元は、Microsoft Authenticode テクノロジを使用して、ドライバー パッケージを署名できます。 このプロセスの詳細については、次を参照してください。[パブリック リリース用のドライバーの署名](signing-drivers-for-public-release.md)します。

 

 

 





