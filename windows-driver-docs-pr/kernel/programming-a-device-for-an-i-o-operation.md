---
title: I/O 操作のためのデバイスのプログラミング
description: I/O 操作のためのデバイスのプログラミング
ms.assetid: 952b07d8-81e3-40ec-8acd-be1143a7d2a2
keywords:
- クリティカル セクション ルーチン WDK カーネル
- I/O WDK カーネル、デバイスのプログラミング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62d4a425124dcdca06df6766ef70c17448edd0e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378788"
---
# <a name="programming-a-device-for-an-io-operation"></a>I/O 操作のためのデバイスのプログラミング





次の一般的なガイドラインを使用して、設計、書き込み、および呼び出しの[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine) I/O 操作のデバイスのプログラミング ルーチン。

-   A *SynchCritSection* I/O 操作のデバイスをプログラムするルーチンができるだけ早く制御を返す必要があります。

    このため、 *SynchCritSection*ルーチンは、I/O のデバイスを設定する必要なだけ行う必要があります。 すべて IRP の前処理、他のドライバーのルーチンの状態情報を初期化およびを呼び出す前に、ハードウェア リソースを取得そのため、ドライバーを実行する必要があります、 *SynchCritSection*ルーチン。

-   デバイス ドライバーでは複数*SynchCritSection*デバイスのプログラミング ルーチンです。

    などの読み取り要求の設定とは異なる著しく特定デバイス制御要求の設定からデバイスのドライバーが個別あります*SynchCritSection*要求の種類ごとにそのデバイスのプログラミング ルーチンです。

-   すべて*SynchCritSection*ルーチン返す必要があります制御可能な限り、早く実行しているため、 *SynchCritSection*ルーチンが、ドライバーの ISR 実行されないようにします。

    1 つの大規模で汎用を記述しないでください*SynchCritSection*ルーチンを**スイッチ**または複数のステートメントが入れ子になった**場合..そうしたら..else**ステートメントを実行するどのような操作または更新するには、どのような状態情報を判断します。 多数の書き込みを避ける必要がありますこれに対して、 *SynchCritSection*ルーチン プログラムの 1 つのデバイスを登録します。

 

 




