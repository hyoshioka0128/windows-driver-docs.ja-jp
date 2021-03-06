---
title: WdbgExts の入力と出力
description: WdbgExts の入力と出力
ms.assetid: 5648b509-7bdd-4d2a-947f-db55a8c69100
keywords:
- 入力、WdbgExts 拡張機能
- WdbgExts 拡張機能を出力します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01825ac56348d7f814e6658eb2ae6fd754b0e729
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369439"
---
# <a name="wdbgexts-input-and-output"></a>WdbgExts の入力と出力


このトピックでは、入力と出力の概要は WdbgExts API を使用して実行できます。 入力と出力のストリームの概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[入力し、出力](input-and-output.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

関数[ **dprintf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_output_routine)標準の C と同様の方法で動作**printf**機能し、デバッガー コマンド ウィンドウに書式設定された文字列を出力しますまたはより正確には、書式設定された文字列に送信される、[コールバックを出力](using-input-and-output.md#output-callbacks)します。 関数を使用するデバッガー エンジンからの入力行を読み取り、 [ **GetInputLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getinputline)します。

ユーザーによる割り込みを確認するには、使用[ **CheckControlC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_check_control_c)します。 この関数は、ユーザーが拡張機能の実行をキャンセルしようとしたかどうかを判断するループ内で使用する必要があります。

強力な入力と出力の API では、次を参照してください。[を使用して入力と出力](using-input-and-output.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





