---
title: I/O 要求の受信
description: I/O 要求の受信
ms.assetid: 0bd41b7b-d64e-4d02-ab5c-0188e926c8e1
keywords:
- I/O 要求の受信の WDK KMDF
- WDK KMDF を要求する I/O の受信
- 要求の WDK KMDF、受信要求の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a1f53df10d9195dffb0c2821816aed56ad5fd27
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390039"
---
# <a name="receiving-io-requests"></a>I/O 要求の受信


フレームワーク ベースのドライバーが使用されている場合、[シーケンシャル](dispatching-methods-for-i-o-requests.md#sequential-dispatching)または[並列](dispatching-methods-for-i-o-requests.md#parallel-dispatching)I/O キューのメソッドのディスパッチが I/O 要求をキューから受信する入力引数としてその[要求ハンドラー](request-handlers.md).

フレームワーク ベースのドライバーが使用されている場合、[手動](dispatching-methods-for-i-o-requests.md#manual-dispatching)I/O キューのメソッドのディスパッチ、I/O 要求から取得、キューのキューをポーリングすることによって。

ドライバーは、要求を受信した後、[を所有する](request-ownership.md)まで要求[requeues](requeuing-i-o-requests.md)、[が完了すると](completing-i-o-requests.md)、[キャンセル](canceling-i-o-requests.md)、または[転送](forwarding-i-o-requests.md)要求。

 

 





