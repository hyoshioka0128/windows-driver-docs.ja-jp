---
title: ミニドライバーの同期
description: ミニドライバーの同期
ms.assetid: 2f560e7a-4717-4b3f-9513-e34fcb2b5e6c
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 カーネルの同期
- ミニドライバー WDK Windows 2000 のカーネル、同期のストリーミング
- ミニドライバー WDK Windows 2000 カーネル ストリーミング、同期
- WDK ストリーミング ミニドライバーの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffa765cb1a49fce79ac73cac13fc1402b770d26d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363298"
---
# <a name="minidriver-synchronization"></a>ミニドライバーの同期





ストリーミングのミニドライバーの開発者には、同期を処理するクラス ドライバーを許可するオプションがあります。 設定クラス ドライバー提供の同期を選択できますミニドライバーは、クラス ドライバーを使用したそのものを登録するときに、 **TurnOffSynchronization**のメンバー [ **HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)に**FALSE**します。

クラス ドライバーは、同期を処理するときに 2 つのミニドライバー コードが同時に実行されることになります。 クラス ドライバーは、ストリームのすべての要求をキューし、それらを一度に 1 つミニドライバーに渡します。

この同期の 1 つの目的は、ドライバの同期とマルチプロセッサ環境のマルチタス キング、再入可能でキューの要求のすべての詳細を処理することから、ミニドライバー ライターにです。 ただし、いくつかのミニドライバーでは、その使用はできません。 2 つの例が記載、[同期例](synchronization-examples.md)同期について行う必要があります、ミニドライバーを説明するトピック。

ストリーム クラスの同期はすべての要求直後および非同期的に呼び出されるパッシブで送信スレッドのコンテキストでミニドライバーをオフにすると\_レベル。 上記の規則の例外は、HwCancelPacket、TimeoutHandler、およびタイマーのルーチンです。 これらは、ディスパッチに呼び出されます。\_レベル。 最終的な例外は、DIRQL で呼ばれる、割り込みハンドラーです。

同期が無効にすると、ミニドライバーは WDM モデルに準拠している同期を実行する責任を負います。 場合、ミニドライバーはパッシブでコールバック\_レベル、Dpc、割り込みより高い IRQL イベントによって、割り込まれることができます。 同様に、ディスパッチに戻り、ミニドライバーが呼び出された場合\_レベル、割り込みによって、その後割り込まれることができます。 共有リソースを操作するミニドライバー関数は、アクセスを同期する必要があります。

複数の要求に同時に実行できる同じまたは別のストリームにストリーム クラスの同期がオフの場合。 ミニドライバーは、独自の要求をキューし、ISR とその他のスレッドのハードウェアの同期を処理する必要があります。 スピンロック、ミュー テックス、および[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)ストリーム ミニドライバーのストリーム クラス同期せずに実行する同期オブジェクトのいくつか利用します。

 

 




