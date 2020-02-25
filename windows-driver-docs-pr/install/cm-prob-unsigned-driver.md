---
title: CM_PROB_UNSIGNED_DRIVER
description: CM_PROB_UNSIGNED_DRIVER
ms.assetid: 91d37d25-ca0d-413f-9e6f-5a22a0406714
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a895d80e88c10f175a080bf5c160fb0570896a
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558412"
---
# <a name="cm_prob_unsigned_driver"></a>CM_PROB_UNSIGNED_DRIVER

この関数は、システムで使用するために予約されています。

デバイスは、デジタル署名されていないドライバーがあるため、64ビットバージョンの Windows で開始されませんでした。 ドライバーに署名する方法の詳細については、「[ドライバーの署名](driver-signing.md)」を参照してください。

## <a name="error"></a>エラー

52

### <a name="display-message"></a>メッセージの表示

"このデバイスに必要なドライバーのデジタル署名を確認できません。 最近のハードウェアまたはソフトウェアの変更により、正しく署名されていないか破損しているファイルがインストールされたか、または不明なソースからの悪意のあるソフトウェアである可能性があります。 (コード 52) "

### <a name="recommended-resolution"></a>推奨される解決策

ドライバーは、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠していません。

エンドユーザーの場合、このエラーを回避する唯一の方法は、デジタル署名されたデバイスのドライバーを入手してインストールすることです。

ドライバー開発者は、さまざまな方法を使用して、64ビット版の Windows に署名されていないドライバーを読み込むことができます。 詳細については、「[開発およびテスト中の署名](installing-an-unsigned-driver-during-development-and-test.md)されていないドライバーのインストール」を参照してください。

## <a name="see-also"></a>参照

[コードの整合性診断システムログイベント](https://docs.microsoft.com/windows-hardware/drivers/install/code-integrity-diagnostic-system-log-events)
