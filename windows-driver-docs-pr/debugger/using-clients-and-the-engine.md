---
title: クライアントとエンジンの使用
description: クライアントとエンジンの使用
ms.assetid: 899184f5-334b-4fd1-98ce-64475650ace5
keywords:
- DbgEng 拡張機能、エンジンクライアントオブジェクト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0eb987d20c73a55f46bb2e3ca0092bf275842f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834220"
---
# <a name="using-clients-and-the-engine"></a>クライアントとエンジンの使用


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


DbgEng 拡張機能は、クライアントオブジェクトを介して[デバッガーエンジン](introduction.md#debugger-engine)とやり取りします。

拡張関数が呼び出されると、クライアントが渡されます。 拡張関数は、他のクライアントを使用する特別な理由がない限り、デバッガーエンジンとのすべての対話にこのクライアントを使用する必要があります。

拡張ライブラリでは、 [**Debugcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugcreate)を使用することにより、初期化時に独自のクライアントオブジェクトを作成できます。 このクライアントを使用して、DLL からコールバックオブジェクトを登録できます。

拡張機能に渡されたクライアントを変更する場合は、**注意**が必要  。 特に、このクライアントにコールバックを登録すると、デバッガーの入力、出力、またはイベントの処理が中断される可能性があります。 コールバックを登録するには、新しいクライアントを作成することをお勧めします。

 

 

 





