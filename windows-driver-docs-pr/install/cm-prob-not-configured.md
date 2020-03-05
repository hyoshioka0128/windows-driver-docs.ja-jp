---
title: CM_PROB_NOT_CONFIGURED
description: CM_PROB_NOT_CONFIGURED
ms.assetid: 8bdc741c-6e1e-46ab-ab2d-fafe87bbd99f
keywords:
- CM_PROB_NOT_CONFIGURED
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2af9e3bbf74db543a7ed9209bff90f519f3cb564
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279515"
---
# <a name="code-1---cm_prob_not_configured"></a>コード 1-CM_PROB_NOT_CONFIGURED

このデバイスマネージャーエラーメッセージは、 **Configflags**レジストリエントリがないデバイスがシステムに存在することを示します。 これは、ドライバーがインストールされていないことを意味します。 通常、これは INF ファイルが見つからなかったことを意味します。

## <a name="error-code"></a>エラー コード

1

### <a name="display-message"></a>メッセージの表示

"このデバイスは正しく構成されていません。 (コード 1) "

"このデバイスのドライバーを更新するには、[ドライバーの更新] をクリックします。 それでもうまくいかない場合は、ハードウェアのドキュメントで詳細を確認してください。 "

### <a name="recommended-resolution"></a>推奨される解決策

**[ドライバーの更新]** を選択すると、ハードウェアの更新ウィザードが起動します。

## <a name="for-driver-developers"></a>ドライバー開発者向け

このエラーは、PnP がデバイスをインストールしようとしていないことを示します。 インストールを再試行します。

この問題の状態が[バグチェック 0x7B: INACCESSIBLE_BOOT_DEVICE](../debugger/bug-check-0x7b--inaccessible-boot-device.md)と共に発生し、デバイスがブートディスクへのパスにある場合、システムには起動に不可欠なデバイス用のドライバーがありません。
