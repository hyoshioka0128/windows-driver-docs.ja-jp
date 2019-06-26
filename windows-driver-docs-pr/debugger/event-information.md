---
title: イベント情報
description: イベント情報
ms.assetid: e6621b5d-f1af-4021-8832-43f79835a6c1
keywords:
- ターゲット、イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f5b337cdbc368d49faead7ef92d2a92db39498
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361369"
---
# <a name="event-information"></a>イベント情報


デバッグ セッションがアクセスできる場合は、*最後のイベント*します。 これは、アクセスできるように、セッションの原因となったイベントです。 *イベント ターゲット*最後のイベントの生成対象となっています。 セッションがアクセス可能になると、現在のターゲットは、イベントのターゲットに設定されます。 最後のイベントの詳細については、によって返される[ **GetLastEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getlasteventinformation)します。 最後のイベントとイベントが発生した命令ポインターでメモリの命令ポインターがによって返される、 [**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-get-captured-event-code-offset)と[**デバッグ\_要求\_読み取る\_CAPTURED\_イベント\_コード\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-read-captured-event-code-stream)します。

ターゲットが、クラッシュ ダンプ ファイルの場合、*最後のイベント*はダンプ ファイルが作成される前に発生した最後のイベントです。 このイベントは、ダンプ ファイルに格納し、エンジン生成、イベント コールバックをデバッグ ターゲットとしてダンプ ファイルが取得されるときにします。

ターゲットがカーネル モードの対象である場合、*バグ チェック*が発生したバグ チェック コードと関連するパラメーターがあります[ **ReadBugCheckData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-readbugcheckdata)します。

ユーザー モードのミニダンプをターゲットには、ダンプのファイル ジェネレーターは、追加のイベントを格納できます。 通常、これは、ダンプ ファイルを保存するジェネレーターを発行するイベントです。 このイベントの詳細については、によって返される[ **GetStoredEventInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)と[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[ **デバッグ\_要求\_ターゲット\_例外\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-context)、 [**デバッグ\_要求\_ターゲット\_例外\_スレッド**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-thread)、および[**デバッグ\_要求\_ターゲット\_例外\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-record).

ダンプ ファイルには、イベントの静的リストを含めることができます。 各イベントは、特定の時点で、ターゲットのスナップショットを表します。 この一覧のイベントの数がによって返される[ **GetNumberEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberevents)します。 リスト内の各イベントの説明は、使用[ **GetEventIndexDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-geteventindexdescription)します。 現在のイベントとしては、この一覧からイベントを設定するには、メソッドを使用して[ **SetNextEventIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setnexteventindex); 呼び出した後[ **WaitForEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)、イベントでは、現在のイベントになります。 イベントの一覧では、現在のイベントを調べるには[ **GetCurrentEventIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenteventindex)します。

 

 





