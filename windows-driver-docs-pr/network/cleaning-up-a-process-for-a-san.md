---
title: SAN のプロセスのクリーンアップ
description: SAN のプロセスのクリーンアップ
ms.assetid: a6ae5882-4cde-43cf-8814-ea7ef5acee58
keywords:
- SAN は、WDK のクリーンアップを処理します。
- SAN プロセス WDK のクリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb500a6110faf1eb791207d19128817e5bc84d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353300"
---
# <a name="cleaning-up-a-process-for-a-san"></a>SAN のプロセスのクリーンアップ





アプリケーションが実行されているプロセスをクリーンアップする準備ができたら、Windows Sockets スイッチへの呼び出しを開始します。 **WSPCleanup**関数。 スイッチはさらに、呼び出し、 [ **WSPCleanup** ](https://msdn.microsoft.com/library/windows/hardware/ff566270) TCP/IP プロバイダーと SAN サービス プロバイダーのすべての関数。 すべてのプロバイダーは、使用していたすべてのリソースを解放する必要があります。 リソースには、たとえば、イベントを同期するために使用するオブジェクトとデータ転送を実行するために使用するメモリが含まれます。

 

 





