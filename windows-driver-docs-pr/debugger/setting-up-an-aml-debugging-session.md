---
title: AML デバッグ セッションの設定
description: AML デバッグ セッションの設定
ms.assetid: 04a44b92-215c-4735-9724-2b9f173f76a2
keywords:
- AMLI デバッガー, セットアップ
- acpi.sys のチェック ビルド (デバッグ ビルド)
- acpi.sys
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: effab9f82549908bf58ea6e563888bb37baf1bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342518"
---
# <a name="setting-up-an-aml-debugging-session"></a>AML デバッグ セッションの設定


## <span id="ddk_setting_up_an_aml_debugging_session_dbg"></span><span id="DDK_SETTING_UP_AN_AML_DEBUGGING_SESSION_DBG"></span>


Acpi.sys で AMLI デバッガーのコードが含まれています。 AML デバッグを完全に実行するためには通常、ターゲット コンピューターでこのドライバーをインストールする必要があります。

無料のビルドでのデバッガーの中断を有効にするには、使用、 **! amli 設定 dbgbrkon** AMLI デバッガー拡張機能の一部であるコマンド。 詳細については、次を参照してください。 [ **! amli セット**](-amli-set.md)します。

 
## <a name="see-also"></a>参照

[AMLI デバッガー](the-amli-debugger.md)

