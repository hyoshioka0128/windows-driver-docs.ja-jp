---
title: イベント
description: イベント
ms.assetid: 2b086e78-ac4d-4f9c-a006-65f6f50b33f1
keywords:
- デバッガーエンジン, イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be9ae2e40e695b29b29c4fb08f093aabd6edbbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826535"
---
# <a name="events"></a>イベント


## <span id="events"></span><span id="EVENTS"></span>


デバッガーエンジンには、ターゲットのイベントを監視して応答する機能が用意されています。 イベントが発生すると、エンジンはターゲットを中断し (多くの場合、短時間のみ)、イベントのすべてのクライアントに通知します。次に、ターゲットで実行を進める方法をエンジンに指示します。

クライアントにイベントを通知するために、エンジンは、クライアントに登録されているイベントコールバックオブジェクトを呼び出します。 エンジンは、イベントの詳細と共に各イベントコールバックを提供します。イベントコールバックは、ターゲットでの実行の進行状況をエンジンに指示します。 異なるイベントコールバックによって命令が競合する場合、エンジンは最も優先順位の高い命令を処理します (「 [**DEBUG\_STATUS\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-status-xxx))」を参照してください。通常は、最小値を含む命令を選択します。ターゲットの実行。

イベントコールバックがイベントを処理している間、ターゲットが中断され、デバッグセッションにアクセスできる**ことに注意**してください  ただし、エンジンは、 [**waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)の呼び出し中に明示的に、または[**g (開始)** ](g--go-.md)や[**p (ステップ)** ](p--step-.md)などのコマンドを実行して暗黙的にイベントを待機していたため、イベントコールバックは**waitforevent**を呼び出すことができません。デバッガーが実行されるコマンド ( **g (開始)** や**p (ステップ) など)** の実行を試みます。エンジンは、これらのコマンドを、続行するための指示として解釈します。

 

### <a name="span-idevent_filtersspanspan-idevent_filtersspanevent-filters"></a><span id="event_filters"></span><span id="EVENT_FILTERS"></span>イベントフィルター

デバッガーエンジンには、*イベントフィルター*も用意されています。これは、基本的なイベント監視の代替手段です。 イベントフィルターには、イベントをデバッガーの出力ストリームに出力するか、デバッガーに分割するかを指定する、いくつかの単純なルールが用意されています。 また、イベントが発生したときにデバッガーコマンドを実行するために使用することもできます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントの監視の詳細については、「[イベントの監視](monitoring-events.md)」を参照してください。

 

 





