---
title: イベント情報
description: イベント情報
ms.assetid: e6621b5d-f1af-4021-8832-43f79835a6c1
keywords:
- ターゲット、イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 247ce0fcbf7430fc22ff069e7733ed41a9baefe5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379498"
---
# <a name="event-information"></a>イベント情報


デバッグ セッションがアクセスできる場合は、*最後のイベント*します。 これは、アクセスできるように、セッションの原因となったイベントです。 *イベント ターゲット*最後のイベントの生成対象となっています。 セッションがアクセス可能になると、現在のターゲットは、イベントのターゲットに設定されます。 最後のイベントの詳細については、によって返される[ **GetLastEventInformation**](https://msdn.microsoft.com/library/windows/hardware/ff546982)します。 最後のイベントとイベントが発生した命令ポインターでメモリの命令ポインターがによって返される、 [**要求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[**デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット**](https://msdn.microsoft.com/library/windows/hardware/ff541561)と[**デバッグ\_要求\_読み取る\_CAPTURED\_イベント\_コード\_ストリーム**](https://msdn.microsoft.com/library/windows/hardware/ff541572)します。

ターゲットが、クラッシュ ダンプ ファイルの場合、*最後のイベント*はダンプ ファイルが作成される前に発生した最後のイベントです。 このイベントは、ダンプ ファイルに格納し、エンジン生成、イベント コールバックをデバッグ ターゲットとしてダンプ ファイルが取得されるときにします。

ターゲットがカーネル モードの対象である場合、*バグ チェック*が発生したバグ チェック コードと関連するパラメーターがあります[ **ReadBugCheckData**](https://msdn.microsoft.com/library/windows/hardware/ff553517)します。

ユーザー モードのミニダンプをターゲットには、ダンプのファイル ジェネレーターは、追加のイベントを格納できます。 通常、これは、ダンプ ファイルを保存するジェネレーターを発行するイベントです。 このイベントの詳細については、によって返される[ **GetStoredEventInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff548431)と[**要求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[ **デバッグ\_要求\_ターゲット\_例外\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff541606)、 [**デバッグ\_要求\_ターゲット\_例外\_スレッド**](https://msdn.microsoft.com/library/windows/hardware/ff541623)、および[**デバッグ\_要求\_ターゲット\_例外\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff541616).

ダンプ ファイルには、イベントの静的リストを含めることができます。 各イベントは、特定の時点で、ターゲットのスナップショットを表します。 この一覧のイベントの数がによって返される[ **GetNumberEvents**](https://msdn.microsoft.com/library/windows/hardware/ff547906)します。 リスト内の各イベントの説明は、使用[ **GetEventIndexDescription**](https://msdn.microsoft.com/library/windows/hardware/ff546630)します。 現在のイベントとしては、この一覧からイベントを設定するには、メソッドを使用して[ **SetNextEventIndex**](https://msdn.microsoft.com/library/windows/hardware/ff556737); 呼び出した後[ **WaitForEvent**](https://msdn.microsoft.com/library/windows/hardware/ff561229)、イベントでは、現在のイベントになります。 イベントの一覧では、現在のイベントを調べるには[ **GetCurrentEventIndex**](https://msdn.microsoft.com/library/windows/hardware/ff545755)します。

 

 





