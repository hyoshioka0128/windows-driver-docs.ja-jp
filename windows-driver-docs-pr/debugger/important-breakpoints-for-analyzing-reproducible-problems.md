---
title: 再現可能な問題を分析するための重要なブレークポイント
description: 再現可能な問題を分析するための重要なブレークポイント
ms.assetid: 3f501bbe-990a-4f46-ba88-c1fc4b73537f
keywords:
- SCSI ミニポート デバッグ、ブレークポイントと再現性の問題
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f4247798cf2e43288c956ddff66749fb06bf2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553131"
---
# <a name="important-breakpoints-for-analyzing-reproducible-problems"></a>再現可能な問題を分析するための重要なブレークポイント


## <span id="ddk_device_manager_problem_codes_dbg"></span><span id="DDK_DEVICE_MANAGER_PROBLEM_CODES_DBG"></span>


SCSI ミニポート ドライバーをデバッグするときに、次の 3 つのルーチンがブレークポイントを設定すると便利ですがあります。

-   **scsiport! scsiportnotification**

-   **scsiport! spstartiosynchronized**

-   **ミニポート!HwStartIo**

ルーチン**scsiport! scsiportnotification**ミニポートに要求を送信後に直接呼び出されます。 したがってブレークポイントを設定した場合**scsiport! scsiportnotification**し、実行を使用して stack backtrace [ **kb 3**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)ミニポートを受信するかどうかを判断して要求を完了します。 最初のパラメーターが 0 の場合は、要求が完了しました。 最初のパラメーターが 0 以外の場合は、3 番目のパラメーターが完了されていない SCSI 要求ブロック (SRB) のアドレス、および使用することができる場合、 [ **! minipkd.srb** ](-minipkd-srb.md)をさらに分析の拡張機能、状況。

いずれかにブレークポイントを配置する**scsiport! spstartiosynchronized**または**ミニポート!HwStartIo**ミニポートに要求を送信する前に中断が発生します。

 

 





