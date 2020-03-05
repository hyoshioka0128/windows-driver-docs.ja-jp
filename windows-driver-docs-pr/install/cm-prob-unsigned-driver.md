---
title: CM_PROB_UNSIGNED_DRIVER
description: CM_PROB_UNSIGNED_DRIVER
ms.assetid: 91d37d25-ca0d-413f-9e6f-5a22a0406714
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fec56daa34610b85deff3d54ee36bebc7da20b2
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279467"
---
# <a name="code-52---cm_prob_unsigned_driver"></a>コード 52-CM_PROB_UNSIGNED_DRIVER

このデバイスマネージャーエラーメッセージは、デジタル署名されていないドライバーがあるため、デバイスが64ビットバージョンの Windows で開始されなかったことを示します。 ドライバーに署名する方法の詳細については、「[ドライバーの署名](driver-signing.md)」を参照してください。

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
