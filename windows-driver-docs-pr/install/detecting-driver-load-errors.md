---
title: ドライバーの読み込みエラーの検出
description: ドライバーの読み込みエラーの検出
ms.assetid: 1233aa87-067e-4f58-add5-3737f8ddd358
keywords:
- ドライバーの読み込みエラー WDK ドライバーの署名
- エラー WDK ドライバーの署名
- 読み込まれたドライバーの検出
- 読み込みエラー WDK ドライバー署名
- 状態情報 WDK ドライバーの署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b63d84209e7791363954a1eb303ef92f974dba8
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558418"
---
# <a name="detecting-driver-load-errors"></a>ドライバーの読み込みエラーの検出


ドライバーが読み込まれたかどうかを検出するには、デバイスマネージャーでデバイスの状態を確認します。 ドライバーが正しく署名されていないために、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)によってドライバーが読み込まれない場合、デバイスのステータスメッセージは、Windows がドライバーを読み込めなかったこと、およびドライバーが破損しているか見つからないことを示します。 この問題が発生した場合は、[コード整合性診断システムログイベント](code-integrity-diagnostic-system-log-events.md)を使用して、問題を詳しく診断できます。 コード52の詳細については、「 [CM_PROB_UNSIGNED_DRIVER](cm-prob-unsigned-driver.md)」を参照してください。

デバイスマネージャーによって報告されたエラーの完全な一覧については、「[デバイスマネージャーのエラーメッセージ](device-manager-error-messages.md)」を参照してください。

問題コードの詳細については、「 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)」を参照してください。

