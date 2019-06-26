---
title: ISR の削除
description: ISR の削除
ms.assetid: 23d84edb-763f-4383-b05c-832b4249b604
keywords:
- isr を特定の削除、割り込みサービス ルーチン WDK カーネル
- 割り込みオブジェクト WDK カーネルは、isr を特定の削除
- Isr WDK カーネル、isr を特定の削除
- WDK の isr を特定のカーネルを削除します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ebd444eb6c00e9e16e2e529a50a15f5a69419c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373424"
---
# <a name="removing-an-isr"></a>ISR の削除


ドライバーに登録されている ISR を削除できます[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)呼び出して[ **IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterruptex)します。 **IoDisconectInterruptEx**を 1 つ受け取り*パラメーター*ポインターであるパラメーターを[ **IO\_切断\_INTERRUPT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_disconnect_interrupt_parameters)構造体。 構造体のメンバーに使用される値は、ISR を登録するために使用するバージョンによって異なります。

ドライバーは、後でそれを削除する ISR を登録するときに特定の情報を保存する必要があります。 接続の\_行\_ベースおよび CONNECT\_完全\_指定されたバージョンでは、ドライバーがで指定された値を保存する必要があります、 **LineBased.InterruptObject**または**FullySpecified.InterruptObject**のメンバー [ **IO\_CONNECT\_INTERRUPT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_connect_interrupt_parameters)します。 接続の\_メッセージ\_ベース バージョンについては、ドライバーがで指定された値を保存する必要があります、**バージョン**と**MessageBased.ConnectionContext**のメンバー **IO\_CONNECT\_INTERRUPT\_パラメーター**します。

 

 




