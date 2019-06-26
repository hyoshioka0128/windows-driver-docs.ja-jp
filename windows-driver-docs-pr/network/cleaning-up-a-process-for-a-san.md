---
title: SAN のプロセスのクリーンアップ
description: SAN のプロセスのクリーンアップ
ms.assetid: a6ae5882-4cde-43cf-8814-ea7ef5acee58
keywords:
- SAN は、WDK のクリーンアップを処理します。
- SAN プロセス WDK のクリーンアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d88a75364760a1a0c02e3e427d9a51fa89ca9fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382783"
---
# <a name="cleaning-up-a-process-for-a-san"></a>SAN のプロセスのクリーンアップ





アプリケーションが実行されているプロセスをクリーンアップする準備ができたら、Windows Sockets スイッチへの呼び出しを開始します。 **WSPCleanup**関数。 スイッチはさらに、呼び出し、 [ **WSPCleanup** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566270(v=vs.85)) TCP/IP プロバイダーと SAN サービス プロバイダーのすべての関数。 すべてのプロバイダーは、使用していたすべてのリソースを解放する必要があります。 リソースには、たとえば、イベントを同期するために使用するオブジェクトとデータ転送を実行するために使用するメモリが含まれます。

 

 





