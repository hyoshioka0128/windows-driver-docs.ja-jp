---
title: WMI イベントの送信
description: WMI イベントの送信
ms.assetid: 0d5e62f1-b84e-42b7-be40-8665f0b58ba8
keywords:
- WMI WDK カーネル、イベント追跡
- イベント WDK WMI
- WDK WMI のトレース
- WMI イベントの送信
- イベントブロック WDK WMI
- 通知 WDK WMI
- 動的インスタンス名 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39c034afc5f6193bc122ebc0ad0e48980b74b88
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838433"
---
# <a name="sending-wmi-events"></a>WMI イベントの送信





ドライバーは、WMI イベントを使用して、アプリケーションが Irp をポーリングまたは送信することなく、イベントのユーザーモードアプリケーションに通知できます。 ドライバーは、wmi イベントを使用して、エラーログの代わりにではなく、wmi クライアントに例外条件を通知する必要があります。 ドライバーは、Wmicore のデバイスの種類に対して定義されている標準イベントブロックをサポートする必要があります。また、デバイス固有の通知をサポートするために、追加のカスタムイベントブロックを定義して登録することもできます。

イベントブロックは、単純に抽象基本クラスの**イベント**から派生したデータブロックです。 イベントブロックには、データブロックと同じデータを格納することも、空にすることもできます。つまり、イベントブロックにドライバー定義データ項目を含める必要はありません。 イベントブロックにデータが含まれている場合、 **Wnode\_* XXX*** に加えて、データの合計サイズは、レジストリ定義の上限である 1 kb を超えないようにする必要があります。 一般に、イベントが小さいほど、システムパフォーマンスが向上し、よりタイムリーな通知が行われます。 ブロックの定義の詳細については、「 [Wmi データおよびイベントブロックの MOF 構文](mof-syntax-for-wmi-data-and-event-blocks.md)」と「 [Wmi データとイベントブロックの設計](designing-wmi-data-and-event-blocks.md)」を参照してください。

ドライバーは、対応するイベントブロックを\_フラグ\_イベント\_に登録することによって、イベントのサポートを示します。これは、ブロックの[**Wmi Regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)構造体で設定された GUID\_のみです。 ブロックの登録の詳細については、「 [WMI Data Provider としての登録](registering-as-a-wmi-data-provider.md)」を参照してください。

WMI クライアントユーザーがイベントの通知を要求すると、WMI は[**IRP\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)を送信し、ドライバーに対して\_EVENTS 要求を有効にします。これにより、ドライバーによって決定されたイベントのトリガー条件の監視が開始されます。 次に、トリガーの条件が発生すると、ドライバーが WMI にイベントを送信します。これにより、イベントに登録されているすべてのデータコンシューマーにイベントが配信されます。

ドライバーは、次のいずれかの方法で WMI にイベントを送信します。

- カーネルモードの WMI ライブラリルーチン[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)を呼び出します。 ドライバーは**WmiFireEvent**を呼び出すことで、動的なインスタンス名を使用しないイベントのみを送信できます。また、1つのベース名文字列または PDO のデバイスインスタンス ID で、静的インスタンス名を指定することもできます。 さらに、イベントは1つのインスタンスである必要があります。つまり、1つの項目または複数のインスタンスで構成されるイベントを送信するために、ドライバーが**WmiFireEvent**を呼び出すことはできません。 詳細については、「 [WmiFireEvent を使用したイベントの送信](sending-an-event-with-wmifireevent.md)」を参照してください。

- ドライバーによって割り当てられ初期化された**Wnode\_* XXX*** 構造体へのポインターを使用して、カーネルモードルーチン[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を呼び出します。この構造には、イベントのデータが含まれます。 詳細については、「 [IoWMIWriteEvent を使用したイベントの送信](sending-an-event-with-iowmiwriteevent.md)」を参照してください。

 

 




