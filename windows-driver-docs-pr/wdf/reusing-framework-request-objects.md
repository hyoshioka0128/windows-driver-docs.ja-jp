---
title: フレームワーク要求オブジェクトの再利用
description: フレームワーク要求オブジェクトの再利用
ms.assetid: 9e3090a9-62d0-48b3-9f3b-7171dc6d2766
keywords:
- 要求の処理の WDK KMDF、要求オブジェクトを再利用
- 要求オブジェクト WDK KMDF、再利用
- WDK KMDF をオブジェクトの要求を再利用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b008c93d1eb95efa1371891271b4887aee5b666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578120"
---
# <a name="reusing-framework-request-objects"></a>フレームワーク要求オブジェクトの再利用





パフォーマンスを向上させるのには、framework ベースのドライバーを作成し、再利用できる大量の I/O をターゲットとほぼ同じ非同期要求を送信は、要求ごとに新しい要求オブジェクトを作成する代わりにオブジェクトを要求します。 ドライバーは、要求が完了した後、要求オブジェクトを再利用できます。

ドライバーが呼び出すことによって、要求オブジェクトを作成してかどうか[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)または[ **WdfRequestCreateFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549953)要求を再利用できます呼び出して[ **WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)します。 ドライバーには、その I/O キューのフレームワークから受信した要求オブジェクトが再利用もできますが、受信した要求オブジェクトに含まれる IRP を変更することはできません。

説明されている失敗した場合の戻り値の発生状況を回避するように注意する場合は[ **WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)、呼び出すことができます、ドライバー **WdfRequestReuse**内から、[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数。 (、 *CompletionRoutine*コールバック関数が VOID の戻り値し、そのため、エラーを報告することはできません)。

お使いのドライバーの場合、 [ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)ドライバーに呼び出す必要がありますが再利用する要求オブジェクトのコールバック関数、 [ **WdfRequestSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff550030)呼び出した後[ **WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)します。

 

 





