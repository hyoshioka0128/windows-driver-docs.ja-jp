---
title: WdbgExts の入力と出力
description: WdbgExts の入力と出力
ms.assetid: 5648b509-7bdd-4d2a-947f-db55a8c69100
keywords:
- WdbgExts 拡張機能、入力
- WdbgExts 拡張機能、出力
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c0f40e285f76cc23e5d625cc70f6888ed16207
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838796"
---
# <a name="wdbgexts-input-and-output"></a>WdbgExts の入力と出力


このトピックでは、WdbgExts API を使用して入力と出力を実行する方法の概要について説明します。 [デバッガーエンジン](introduction.md#debugger-engine)での入出力ストリームの概要については、このドキュメントの「[デバッガーエンジンの概要](debugger-engine-overview.md)」セクションの「[入力と出力](input-and-output.md)」を参照してください。

関数[**dprintf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_output_routine)は、標準の C **printf**関数と同様の方法で動作し、書式設定された文字列をデバッガーに出力コマンドウィンドウまたはより正確には、書式設定された文字列を[出力コールバック](using-input-and-output.md#output-callbacks)に送信します。 デバッガーエンジンから入力行を読み取るには、 [**Getinputline**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getinputline)関数を使用します。

ユーザーが開始した割り込みを確認するには、 [**Checkcontrolc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_check_control_c)を使用します。 この関数は、ユーザーが拡張機能の実行をキャンセルしようとしたかどうかを判断するために、ループで使用する必要があります。

より強力な入力および出力 API については、このドキュメントの「[デバッガーエンジン API を使用](using-the-debugger-engine-api.md)したの[入力と出力の使用](using-input-and-output.md)」を参照してください。

 

 





