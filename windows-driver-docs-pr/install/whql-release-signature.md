---
title: WHQL リリース署名
description: WHQL リリース署名
ms.assetid: edc815d4-596c-4f50-9bff-029b8ea19a0a
keywords:
- ドライバーの署名の WDK、WHQL のデジタル署名
- 署名ドライバー WDK、WHQL のデジタル署名
- デジタル署名 WDK、WHQL
- WDK、WHQL の署名
- WHQL 署名 WDK
- パブリック リリースのドライバー WDK、WHQL 署名
- WDK、WHQL 署名をリリースします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c3e11cec40da6182eb3e5e9e2c2799adfe30875
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363514"
---
# <a name="whql-release-signature"></a>WHQL リリース署名


[Windows ハードウェア認定キット (HCK)](driver-packages.md) のテストに合格した[ドライバー パッケージ](https://go.microsoft.com/fwlink/p/?linkid=254893)は、WHQL でデジタル署名することができます。 を介して配信できる場合は、ドライバー パッケージが WHQL によってデジタル署名が、 [Windows Update](https://docs.microsoft.com/windows-hardware/drivers)プログラムまたはその他の Microsoft でサポートされている配布メカニズム。

WHQL リリース署名の取得は、[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) の一部です。 WHQL リリース署名は、デジタル署名された[カタログ ファイル](catalog-files.md)から成ります。 テスト向けに提出するドライバーのバイナリ ファイルや INF ファイルがデジタル署名によって変更されることはありません。

WHQL リリース署名の取得は、以下の構成します。

-   テスト、[ドライバー パッケージ](driver-packages.md)ドライバー パッケージが Microsoft Windows と互換性があることを確認する Windows HCK を使用します。 HCK をインストールすると、テストおよびドライバー パッケージを検証するドライバー テスト Manager (DTM) が実行されます。 詳細については、次を参照してください。、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)します。

-   WHQL を取得するには、Windows Quality Online Services への送信の DTM テスト ログは、ドライバー パッケージの署名をリリースします。 詳細については、次を参照してください。、 [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)します。

WHQL の詳細については、次を参照してください。、 [Windows Hardware Quality Labs](https://go.microsoft.com/fwlink/p/?linkid=8705) web サイト。

**注**  WHQL ドライバー ファイルの署名が埋め込まれません。 サード パーティの商用を使用してドライバー ファイルの署名を埋め込むことができます[リリース証明書](release-certificates.md)します。 WHQL するドライバー パッケージを送信する前に、ドライバー ファイルに署名を埋め込みます。

 

 

 





