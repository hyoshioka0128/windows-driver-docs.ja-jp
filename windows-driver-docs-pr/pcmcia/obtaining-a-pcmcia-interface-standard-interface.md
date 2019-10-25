---
title: PCMCIA_INTERFACE_STANDARD インターフェイスを取得する
description: PCMCIA_INTERFACE_STANDARD インターフェイスを取得する
ms.assetid: 475bf66a-5b6e-4a06-95f7-b7280dd7276d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f18880760a6c6bc682ec5a940afed73c5127b2d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837728"
---
# <a name="obtaining-a-pcmcia_interface_standard-interface"></a>標準インターフェイス\_PCMCIA\_インターフェイスを取得する





このセクションでは、pcmcia\_インターフェイス\_pcmcia バスドライバーから pcmcia メモリカードの標準インターフェイスを取得する方法について説明します。

ドライバーは、irp\_MJ\_の PNP 要求を作成して送信することによって、標準インターフェイス\_の PCMCIA\_インターフェイスを取得します。これにより、\_インターフェイスのマイナー関数コード\_、 [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)を実行するように指定します。 ドライバーは、次の操作を実行します。

-   ページングされたメモリプール内の[PCMCIA\_インターフェイス\_標準インターフェイスメモリカードルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の構造体を割り当て、ゼロに設定します。

-   クエリインターフェイス要求の IRP を作成し、新しい IRP の次のスタック位置を取得します。

-   新しいスタック位置に次のメンバーを設定します。
    -   **パラメーターの QueryInterface**メンバーは、ドライバーによって割り当てられた PCMCIA\_インターフェイス\_標準構造体を指します。
    -   **InterfaceType**メンバーは、GUID 値 GUID\_PCMCIA\_INTERFACE\_standard によって、標準の PCMCIA インターフェイスを指定します。
-   完了ルーチンを設定し、ドライバースタックから要求を送信します。

要求が成功した場合、PCMCIA バスドライバーは、**パラメーター. QueryInterface. インターフェイス**によって示されている標準構造\_、PCMCIA\_インターフェイスに入力します。

ドライバーは、ドライバースタックからこの要求を送信するために、IRQL &lt; ディスパッチ\_レベルで実行されている必要があります。

 

 





