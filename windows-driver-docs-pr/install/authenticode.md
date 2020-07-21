---
title: Authenticode デジタル署名
description: Authenticode デジタル署名
ms.assetid: b4cddf64-dc1a-47b7-803d-afb1e175c9d5
keywords:
- Authenticode WDK ドライバー署名
- ドライバー署名 WDK、Authenticode
- 署名ドライバー WDK、Authenticode
- デジタル署名 WDK、Authenticode
- 署名 WDK、Authenticode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e944c9ffb96488b18ffbb42808bb570ec6f9c66
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557763"
---
# <a name="authenticode-digital-signatures"></a>Authenticode デジタル署名


Authenticode は、Authenticode 署名されたソフトウェアの発行元を識別する Microsoft コード署名テクノロジです。 また、Authenticode は、署名および公開されてからソフトウェアが改ざんされていないことを確認します。

Authenticode は暗号手法を使用して、発行元の id とコードの整合性を検証します。 また、デジタル署名と証明機関 (Ca) を含む信頼されたエンティティのインフラストラクチャを組み合わせて、指定された発行元からのドライバーをユーザーに提供することを保証します。 Authenticode では、証明書を信頼されたルート証明書までチェーンすることによって、ソフトウェア発行元の id を確認できます。

Authenticode を使用すると、ソフトウェアの発行元は、ドライバーまたは[ドライバーパッケージ](driver-packages.md)に署名し、発行元の身元を確認する[デジタル証明書](digital-certificates.md)を使用してタグ付けします。また、コードの受信者にコードの整合性を検証する機能も提供します。 証明書は、ソフトウェアの発行元を識別するデータのセットです。 CA によって発行されるのは、その機関がソフトウェア発行元の id を検証した後のみです。 証明書データには、発行元の公開暗号化キーが含まれます。 証明書は通常、このような証明書のチェーンの一部であり、最終的には VeriSign などの既知の CA に参照されます。

Authenticode コード署名では、ドライバーの実行可能部分は変更されません。 代わりに、次のことを行います。

-   署名が埋め込まれている場合は、署名プロセスによって、ドライバーファイルの実行時以外の部分にデジタル署名が埋め込まれます。 このプロセスの詳細については、「[ドライバーファイルに埋め込まれた署名](embedded-signatures-in-a-driver-file.md)」を参照してください。

-   デジタル署名された[カタログファイル](catalog-files.md)(*.cat*) では、署名プロセスで、[ドライバーパッケージ](driver-packages.md)内の各ファイルの内容からファイルハッシュ値を生成する必要があります。 このハッシュ値は、カタログファイルに含まれています。 カタログファイルは、埋め込まれた署名で署名されます。 このように、カタログファイルはデタッチされた署名の一種です。

**メモ**   [ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)には、さまざまな種類のデバイスのテストカテゴリがあります。 テストカテゴリの一覧については、「 [HLK API Reference](https://docs.microsoft.com/windows-hardware/test/hlk/api/hlk-api-reference)」を参照してください。 この一覧にデバイスの種類のテストカテゴリが含まれている場合、ソフトウェア発行元は、[ドライバーパッケージ](driver-packages.md)の[WHQL リリース署名](whql-release-signature.md)を取得する必要があります。ただし、HCK にデバイスの種類のテストプログラムがない場合、ソフトウェア発行者は Microsoft Authenticode テクノロジを使用してドライバーパッケージに署名できます。 このプロセスの詳細については、「[パブリックリリースのドライバー](signing-drivers-for-public-release--windows-vista-and-later-.md)への署名」を参照してください。

 

 

 





