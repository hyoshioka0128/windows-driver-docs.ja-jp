---
title: AML デバッグ セッションの設定
description: AML デバッグ セッションの設定
ms.assetid: 04a44b92-215c-4735-9724-2b9f173f76a2
keywords:
- AMLI デバッガー、セットアップ
- acpi のデバッグビルド
- acpi
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f63b976e3866f9a284636651e6722b52d62f4fdc
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209788"
---
# <a name="setting-up-an-aml-debugging-session"></a>AML デバッグ セッションの設定


## <span id="ddk_setting_up_an_aml_debugging_session_dbg"></span><span id="DDK_SETTING_UP_AN_AML_DEBUGGING_SESSION_DBG"></span>


AMLI デバッガーコードは、Acpi に含まれています。 AML デバッグを完全に実行するには、このドライバーがターゲットコンピューターにインストールされている必要があります (通常は)。

フリービルドでデバッガーの中断をアクティブにするには、AMLI デバッガー拡張機能の一部である **! amli set dbgbrkon**コマンドを使用します。 詳細については、「 [**! amli set**](-amli-set.md)」を参照してください。

 
## <a name="see-also"></a>参照

[AMLI デバッガー](the-amli-debugger.md)
