---
title: イベント情報
description: イベント情報
ms.assetid: e6621b5d-f1af-4021-8832-43f79835a6c1
keywords:
- ターゲット、イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a373e53893e91a710ede1967210d5f041080a73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837753"
---
# <a name="event-information"></a>イベント情報


デバッグセッションにアクセスできる場合は常に、*最後のイベント*が発生します。 これは、セッションがアクセス可能になる原因となったイベントです。 *イベントターゲット*は、最後のイベントを生成したターゲットです。 セッションがアクセス可能になると、現在のターゲットがイベントターゲットに設定されます。 最後のイベントの詳細は、 [**Getlasteventinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getlasteventinformation)によって返されます。 イベントが発生したときの最後のイベントの命令ポインターと命令ポインターのメモリは、[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作デバッグ\_要求によって返され、[**イベント\_コード\_取得\_キャプチャされ\_\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-get-captured-event-code-offset)および[**デバッグ\_要求\_読み取り\_\_キャプチャされたイベント\_コード\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-read-captured-event-code-stream)。

ターゲットがクラッシュダンプファイルの場合、最後の*イベント*はダンプファイルが作成される前に発生した最後のイベントです。 このイベントはダンプファイルに格納され、ダンプファイルがデバッグターゲットとして取得されるときに、エンジンによってイベントコールバック用に生成されます。

ターゲットがカーネルモードターゲットであり、*バグチェック*が発生した場合は、 [**Readbug checkdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-readbugcheckdata)を使用してバグチェックコードと関連パラメーターを見つけることができます。

ターゲットがユーザーモードミニダンプの場合、ダンプファイルジェネレーターは追加のイベントを格納することがあります。 通常、これは、ダンプファイルを保存するジェネレーターを引き起こしたするイベントです。 このイベントの詳細は[**GetStoredEventInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getstoredeventinformation)によって返され、[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作によって[**デバッグ\_要求\_ターゲット\_例外\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-context)、[**デバッグ\_要求\_ターゲット\_EXCEPTION\_THREAD**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-thread)、および[**DEBUG\_REQUEST\_ターゲット\_例外\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-target-exception-record)です。

ダンプファイルには、イベントの静的なリストを含めることができます。 各イベントは、特定の時点でのターゲットのスナップショットを表します。 この一覧に含まれるイベントの数は、 [**Getnumber イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberevents)によって返されます。 リスト内の各イベントの説明を表示するには、 [**Geteventindexdescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteventindexdescription)を使用します。 この一覧からイベントを現在のイベントとして設定するには、 [**Setnexteventindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setnexteventindex); メソッドを使用します。[**Waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)を呼び出すと、イベントが現在のイベントになります。 リスト内のどのイベントが現在のイベントであるかを判断するには、 [**Getcurrenteventindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenteventindex)を使用します。

 

 





