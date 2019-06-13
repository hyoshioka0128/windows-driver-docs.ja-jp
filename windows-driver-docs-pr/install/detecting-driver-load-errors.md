---
title: ドライバーの読み込みエラーの検出
description: ドライバーの読み込みエラーの検出
ms.assetid: 1233aa87-067e-4f58-add5-3737f8ddd358
keywords:
- ドライバー ロード エラー WDK ドライバー署名
- WDK のドライバー署名のエラー
- 読み込まれるドライバーの検出
- エラー WDK ドライバーの署名を読み込む
- 状態情報の WDK ドライバーの署名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbf620cdd083b199c39b0305b33bc8c1906ef5c3
ms.sourcegitcommit: ba351c01be491b8ab5c74d778ab02c8766a5667a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041371"
---
# <a name="detecting-driver-load-errors"></a>ドライバーの読み込みエラーの検出


ドライバーが読み込まれているかどうかを検出するためには、デバイス マネージャーでデバイスの状態を確認します。 場合、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)ドライバーのブロックから読み込むと、ドライバーが正しく署名されていないため、デバイスの状態を示すメッセージが Windows ドライバーを読み込むことができませんし、ドライバーが破損する可能性がまたは不足しています。 使用することができます、このような場合[診断システムでログ イベントのコードの整合性](code-integrity-diagnostic-system-log-events.md)問題を詳しく診断します。

次のスクリーン ショットでは、不足している Windows デバイス用のドライバーを読み込むことができません、ドライバーが破損する可能性があることを示すデバイスのステータス メッセージの種類を示します。  デバイス マネージャーによって報告されたエラーの一覧については、次を参照してください。[デバイス マネージャーのエラー メッセージ](device-manager-error-messages.md)します。

![署名されていないドライバーのエラー メッセージのスクリーン ショット](images/signing-driver-load-error-message.png)

 

 





