---
title: ドライバーの読み込みエラーを検出します。
description: ドライバーの読み込みエラーを検出します。
ms.assetid: 1233aa87-067e-4f58-add5-3737f8ddd358
keywords:
- ドライバー ロード エラー WDK ドライバー署名
- WDK のドライバー署名のエラー
- 読み込まれるドライバーの検出
- エラー WDK ドライバーの署名を読み込む
- 状態情報の WDK ドライバーの署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 192340bf06399775b83d66b6b15fdb0635326472
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553770"
---
# <a name="detecting-driver-load-errors"></a>ドライバーの読み込みエラーを検出します。


ドライバーが読み込まれているかどうかを検出するためには、デバイス マネージャーでデバイスの状態を確認します。 場合、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)ドライバーのブロックから読み込むと、ドライバーが正しく署名されていないため、デバイスの状態を示すメッセージが Windows ドライバーを読み込むことができませんし、ドライバーが破損する可能性がまたは不足しています。 使用することができます、このような場合[診断システムでログ イベントのコードの整合性](code-integrity-diagnostic-system-log-events.md)問題を詳しく診断します。

次のスクリーン ショットでは、不足している Windows デバイス用のドライバーを読み込むことができません、ドライバーが破損する可能性があることを示すデバイスのステータス メッセージの種類を示します。

![署名されていないドライバーのエラー メッセージのスクリーン ショット](images/signing-driver-load-error-message.png)

 

 





