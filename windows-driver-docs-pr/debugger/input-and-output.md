---
title: 入力と出力
description: 入力と出力
ms.assetid: 78e181c1-c577-49ca-910b-d2e8db2495b5
keywords:
- デバッガーエンジン、入出力
- 入力と出力
- Output
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90c7131ff684e7436542f7d4f788ac2ab2c3bef7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826400"
---
# <a name="input-and-output"></a>入力と出力


[デバッガーエンジン](introduction.md#debugger-engine)の入出力機能は、対話式のデバッガー操作とログ記録に使用できます。 通常、入力はユーザーが入力したコマンドと応答を表し、出力は通常、ユーザーに提示される情報、またはログファイルに送信される情報を表します。

デバッガーエンジンは、*入力ストリーム*と*出力ストリーム*を保持します。 入力ストリームから入力を要求し、出力ストリームに送信することができます。

[**入力メソッドが**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol-input)呼び出され、エンジンの入力ストリームからの入力を要求すると、エンジンは、入力を待機していることを通知するために、登録されているすべての[入力コールバック](using-input-and-output.md#input-callbacks)を呼び出します。 次に、入力コールバックが[**returninput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-returninput)メソッドを呼び出して入力を提供するまで待機します。

出力がエンジンの出力ストリームに送信されると、エンジンは、出力を渡す登録済みの[出力コールバック](using-input-and-output.md#output-callbacks)を呼び出します。 出力を出力ストリームに送信する場合は、クライアントオブジェクトによってフィルター処理できます。この場合、出力を受け取るのは、特定のクライアントオブジェクトに登録されている出力コールバックだけです。

入力ストリームと出力ストリームは、リモートクライアントから透過的に利用できます。 リモートクライアントは、入力を要求し、エンジンの入力ストリームと出力ストリームに出力を送信できます。また、エンジンは、リモートクライアントに登録されているコールバックを呼び出して、入力を要求したり出力を送信したりします。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

入力と出力の使用方法の詳細については、「[入力と出力の使用](using-input-and-output.md)」を参照してください。 クライアントオブジェクトと入出力コールバックの詳細については、「[クライアントオブジェクト](client-objects.md)」を参照してください。

 

 





