---
title: クライアントとエンジンの使用
description: クライアントとエンジンの使用
ms.assetid: 899184f5-334b-4fd1-98ce-64475650ace5
keywords:
- DbgEng 拡張機能、エンジン クライアント オブジェクト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b704ed709cf8beeba05b3fafb19551138eb62601
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368618"
---
# <a name="using-clients-and-the-engine"></a>クライアントとエンジンの使用


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


DbgEng 拡張機能の対話、[デバッガー エンジン](introduction.md#debugger-engine)クライアント オブジェクトを使用します。

拡張関数が呼び出されると、クライアントが渡されます。 別のクライアントを使用する特定の理由がない限り、拡張関数のすべての対話は、デバッガー エンジンのこのクライアントを使用する必要があります。

拡張ライブラリを使用して初期化時に、独自のクライアント オブジェクトを作成することがあります[ **DebugCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugcreate)します。 このクライアントを使用して、DLL からのコールバック オブジェクトを登録できます。

**注**  拡張関数に渡される、クライアントを変更するときに、注意を実行する必要があります。 具体的には、クライアントのコールバックを登録すると、デバッガーの入力、出力、またはイベントの処理が中断される可能性があります。 コールバックを登録する新しいクライアントを作成することをお勧めします。

 

 

 





