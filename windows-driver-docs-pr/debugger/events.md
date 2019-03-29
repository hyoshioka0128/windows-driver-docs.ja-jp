---
title: イベント
description: イベント
ms.assetid: 2b086e78-ac4d-4f9c-a006-65f6f50b33f1
keywords:
- デバッガー エンジン イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe20756868d9217ce3ca983c65a732502f6ffacc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579858"
---
# <a name="events"></a>イベント


## <span id="events"></span><span id="EVENTS"></span>


デバッガー エンジンは、監視と、ターゲット内のイベントに応答するための機能を提供します。 イベントの発生時に、エンジンの中断 (一時的に多くの場合のみ)、ターゲットにし、すべてのイベントのさらに、ターゲットの実行を続ける方法をエンジンに指示するクライアント通知します。

イベントのクライアントを通知するには、は、エンジンは、クライアントに登録されているイベントのコールバック オブジェクトを呼び出します。 エンジンは、各イベントのコールバック、イベントの詳細を提供し、イベント コールバック ターゲットでの実行を続ける方法をエンジンに指示します。 さまざまなイベントのコールバックは、競合する指示を提供、ときに、エンジンが優先順位が最も高い命令で機能します (を参照してください[**デバッグ\_状態\_XXX**](https://msdn.microsoft.com/library/windows/hardware/ff541651))、通常、ターゲットの最小限の実行が関係する命令を選択することを意味します。

**注**   、イベントを処理するイベントのコールバックも、ターゲットが中断されて、デバッグ セッションにアクセスできるただし、エンジンが--イベント中に明示的にいずれかを待機していたため、 [ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)呼び出すか、コマンドの実行によって暗黙的になど[ **g (移動)** ](g--go-.md)または[ **p (ステップ)** ](p--step-.md)--イベント コールバックを呼び出すことはできません**WaitForEvent**を実行するデバッガーを原因となる任意のコマンドを実行しようとすると、 **g (移動)** または**p (ステップ)** エンジンでは、これらのコマンドは続行方法に関する命令と解釈します。

 

### <a name="span-ideventfiltersspanspan-ideventfiltersspanevent-filters"></a><span id="event_filters"></span><span id="EVENT_FILTERS"></span>イベント フィルター

デバッガー エンジンも用意されています。*イベント フィルター*、基本的なイベントを監視するための簡単な代替手法であります。 イベントのフィルターは、イベントをデバッガーに、デバッガーの出力ストリームまたは中断する印刷かどうかを指定するいくつかの単純なルールを提供します。 また、イベントが発生したときに、デバッガー コマンドを実行することも使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

イベントの監視の詳細については、次を参照してください。[監視イベント](monitoring-events.md)します。

 

 





