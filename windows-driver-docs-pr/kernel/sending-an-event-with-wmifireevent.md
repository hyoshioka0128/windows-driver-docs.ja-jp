---
title: WmiFireEvent でのイベントの送信
description: WmiFireEvent でのイベントの送信
ms.assetid: f9cf8491-0f5a-4d83-849f-3edb77488092
keywords:
- WMI WDK カーネル、イベント追跡
- イベント WDK WMI
- WDK WMI のトレース
- WMI イベントの送信
- イベントブロック WDK WMI
- 通知 WDK WMI
- WmiFireEvent
- 動的インスタンス名 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5303113f4f1ac4bb8c5ccc25eaeb4ab8bc23789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838437"
---
# <a name="sending-an-event-with-wmifireevent"></a>WmiFireEvent でのイベントの送信





ドライバーは、 [**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)を呼び出して、動的インスタンス名を使用しないイベントを送信することができます。また、1つのベース名文字列または PDO のデバイスインスタンス ID で、静的インスタンス名を指定することもできます。

イベントは、ブロックの1つのインスタンスである必要があります。つまり、1つの項目または複数のインスタンスで構成されるイベントを送信するために、ドライバーが**WmiFireEvent**を呼び出すことはできません。 このようなイベントを送信するには、「 [IoWMIWriteEvent を使用](sending-an-event-with-iowmiwriteevent.md)したイベントの送信」で説明されているように、ドライバーは[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を呼び出す必要があります。

ドライバーは、WMI によってイベントが有効になるまでイベントを送信しません。 イベントが有効になった後、イベントのトリガー条件が発生すると、ドライバーは次のようになります。

1.  ページングされていないプールからバッファーを割り当て、イベントデータをバッファーに書き込みます。 イベントにデータがない場合、ドライバーはこの手順をスキップできます。

2.  次のパラメーターを使用して[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)を呼び出します。

    -   ドライバーのデバイスオブジェクトへのポインター

    -   イベントブロックを表す GUID へのポインター

    -   イベントブロックに複数のインスタンスがある場合は、インスタンスのインデックス

    -   データがイベントと共に送信される場合は、データのバイト数。存在しない場合は0。

    -   イベントと共にデータを送信する場合は、データを格納するドライバーで割り当てられたバッファーへのポインター、none の場合は**NULL** 。

    ドライバーは、 **WmiFireEvent**に渡されるすべてのパラメーター (イベントデータバッファーを含む) を非ページプールから割り当てる必要があります。 WMI はドライバーによって割り当てられたメモリを解放します。

**WmiFireEvent**が返された後、ドライバーはイベントのトリガー条件の監視を再開し、WMI がそのイベントを無効にするまで、そのトリガー条件が発生するたびにイベントを送信します。

 

 




