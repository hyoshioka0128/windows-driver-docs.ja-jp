---
title: ISR の削除
description: ISR の削除
ms.assetid: 23d84edb-763f-4383-b05c-832b4249b604
keywords:
- 割り込みサービスルーチンの WDK カーネル、Isr の削除
- 割り込みオブジェクト WDK カーネル、Isr の削除
- Isr WDK カーネル, Isr の削除
- Isr WDK カーネルの削除
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d0a102b7b81e855b535eca61f36d148e075ae7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836471"
---
# <a name="removing-an-isr"></a>ISR の削除


ドライバーは、 [**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)を呼び出すことによって、 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)に登録されている ISR を削除できます。 **IoDisconectInterruptEx**は1つの*パラメーター*パラメーターを受け取ります。これは、 [**IO\_切断\_割り込み\_Parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_disconnect_interrupt_parameters)構造体へのポインターです。 構造体のメンバーに使用される値は、ISR の登録に使用されるバージョンによって異なります。

ドライバーは、ISR を後で削除するために、特定の情報を保存する必要があります。 接続\_ライン\_ベースにして、指定されたバージョン\_\_接続するには、ドライバーは、FullySpecified または**InterruptObject**の IO のメンバーに指定されている値を保存する必要があります **。** [ **\_\_割り込み\_パラメーターに接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)します。 CONNECT\_MESSAGE\_BASED バージョンでは、ドライバーは**バージョン**および**messagebased**に指定された値を保存する必要があります。 **I/O\_接続\_の割り込み\_パラメーター**。

 

 




