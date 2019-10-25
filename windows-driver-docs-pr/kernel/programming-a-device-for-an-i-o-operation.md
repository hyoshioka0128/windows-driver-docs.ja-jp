---
title: I/O 操作のためのデバイスのプログラミング
description: I/O 操作のためのデバイスのプログラミング
ms.assetid: 952b07d8-81e3-40ec-8acd-be1143a7d2a2
keywords:
- クリティカルセクションルーチン WDK カーネル
- I/o WDK カーネル、デバイスプログラミング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52de1a5d3ddc562fb7b97db825d8174442151e04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838485"
---
# <a name="programming-a-device-for-an-io-operation"></a>I/O 操作のためのデバイスのプログラミング





I/o 操作用にデバイスをプログラミングする[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを設計、記述、および呼び出すには、次の一般的なガイドラインを使用します。

-   I/o 操作用にデバイスをプログラムする*SynchCritSection*ルーチンは、できるだけ早く制御を返す必要があります。

    このため、 *SynchCritSection*ルーチンでは、i/o 用にデバイスを設定するために必要なもののみを実行する必要があります。 そのため、ドライバーは、 *SynchCritSection*ルーチンを呼び出す前に、すべての IRP のプリプロセスを実行し、他のドライバールーチンの状態情報を初期化し、ハードウェアリソースを取得する必要があります。

-   デバイスドライバーは、デバイスをプログラミングするために複数の*SynchCritSection*ルーチンを持つことができます。

    たとえば、読み取り要求を設定するデバイスのドライバーは、特定のデバイス制御要求を設定した場合には、要求の種類ごとにデバイスをプログラミングするための個別の*SynchCritSection*ルーチンを持つことがあります。

-   *SynchCritSection*ルーチンを実行すると、ドライバーの ISR が実行されないため、すべての*SynchCritSection*ルーチンはできるだけ早く制御を返す必要があります。

    **Switch**ステートメントを使用して、または入れ子になっ **た if.. を含む、1つの大規模な汎用 SynchCritSection ルーチンを記述しないでください。そうしたら。。else**ステートメントを実行して、実行される操作や更新する状態情報を決定します。 一方、1つのデバイスレジスタだけをプログラミングする多くの*SynchCritSection*ルーチンを記述することは避けてください。

 

 




