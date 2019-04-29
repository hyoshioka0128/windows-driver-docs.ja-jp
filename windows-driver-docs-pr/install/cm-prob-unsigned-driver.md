---
title: CM_PROB_UNSIGNED_DRIVER
description: CM_PROB_UNSIGNED_DRIVER
ms.assetid: 91d37d25-ca0d-413f-9e6f-5a22a0406714
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0fbaa9c4f60ac3b90072c21b24746d8c5287154
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327138"
---
# <a name="cmprobunsigneddriver"></a>CM_PROB_UNSIGNED_DRIVER

この関数は、システムの使用に予約されています。

デジタル署名されていないドライバーがあるために、Windows の 64 ビット バージョンで、デバイスが開始されませんでした。 ドライバーに署名する方法の詳細については、次を参照してください。[ドライバーの署名](driver-signing.md)します。

## <a name="error"></a>[エラー]

52

### <a name="display-message"></a>メッセージを表示します。

"Windows は、このデバイスに必要なドライバーのデジタル署名を確認できません。 最近のハードウェアまたはソフトウェアの変更によってインストールされたファイルが正しく署名されていないか、壊れているか、または不明なソースからの悪意のあるソフトウェアがある可能性があります。 (コード 52)"

### <a name="recommended-resolution"></a>推奨される解決方法

ドライバーは準拠していない、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)します。

このエラーを回避する唯一の方法は、エンドユーザー向けの入手して、デバイスのデジタル署名されたドライバーをインストールするがします。

ドライバー開発者向けの Windows の 64 ビット バージョンで未署名のドライバの読み込みにさまざまなメソッドを使用できます。 詳細については、次を参照してください。[開発およびテスト中に、署名されていないドライバーをインストールする](installing-an-unsigned-driver-during-development-and-test.md)します。
