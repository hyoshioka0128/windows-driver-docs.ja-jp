---
title: Windows カーネルモード カーネル トランザクション マネージャー
description: Windows カーネルモード カーネル トランザクション マネージャー
ms.assetid: 43bf96ed-8be8-4670-a310-99cd7c7f9073
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 016fc60ae26f7b561db03037b6d554dacd8d7b57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372922"
---
# <a name="windows-kernel-mode-kernel-transaction-manager"></a>Windows カーネルモード カーネル トランザクション マネージャー


複数の読み取りを扱うで 1 つまたは複数のデータ ストア、および操作上の書き込みが成功する必要がありますすべてアトミックに、またはデータの整合性を保持するために失敗した場合、操作を単一のトランザクションとしてグループ化する可能性があります。 すべてのトランザクション内で操作が成功した場合は、すべての変更がアトミック単位として保持できるように、トランザクションがコミットできます。 障害が発生する場合は、データ ストアが元の状態に復元されるように、トランザクションがロールバックできます。

カーネル トランザクション マネージャー (KTM) は、カーネル モードでトランザクション処理を実装する Windows カーネル モード コンポーネントです。 KTM は、カーネル モードのコンポーネント、ドライバーは、トランザクションを実行するなどを使用します。 さらに、KTM には、ユーザー モードでプラットフォーム[トランザクション NTFS (TxF)](https://go.microsoft.com/fwlink/p/?linkid=131245)基づきます。

カーネル モードのコンポーネントで KTM を使用する方法については、次を参照してください。[カーネル トランザクション マネージャ](using-kernel-transaction-manager.md)します。

 

 




