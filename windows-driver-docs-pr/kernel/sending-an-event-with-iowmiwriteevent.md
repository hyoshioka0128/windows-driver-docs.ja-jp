---
title: IoWMIWriteEvent イベントでのイベントの送信
description: IoWMIWriteEvent イベントでのイベントの送信
ms.assetid: 77c1041a-340c-4c59-a30a-e946adf60a95
keywords:
- WMI の WDK カーネルでは、イベントの追跡
- WDK の WMI イベント
- WDK の WMI のトレース
- WMI イベントの送信
- イベントは、WDK の WMI をブロックします。
- WDK の WMI の通知
- IoWMIWriteEvent
- WDK の WMI の名前の動的インスタンス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3bb45fea80152dcf5f083e49428097160ea354
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580205"
---
# <a name="sending-an-event-with-iowmiwriteevent"></a>IoWMIWriteEvent イベントでのイベントの送信





ドライバーが呼び出せる[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)任意のイベントを送信します。 1 つの項目、1 つのインスタンス、または、データ ブロックのすべてのインスタンス イベントできますから構成され、動的なインスタンス名を使用できます。

異なり**れた WNODE\_* XXX*** WMI によって部分的に初期化し、割り当てられ、このクエリまたは変更要求で渡された構造体、ドライバーする必要がありますを割り当てるし、のすべてのメンバーの初期化、**れた WNODE\_* XXX*** イベントを含む構造体。

ドライバーは、WMI が送信後にのみイベントを送信する必要があります、 [ **IRP\_MN\_を有効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550859)イベントを有効にする要求。 次に、ときに、イベントのトリガー条件が発生したドライバー。

1. 格納する非ページ プールからバッファーを割り当てます、**れた WNODE\_* XXX*** 存在する場合は、変数のデータの空白を含む、イベントのために必要な構造体。

   イベントに応じて、ドライバーを割り当てることがあります、 [**れた WNODE\_単一\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff566378)、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)、または[**れた WNODE\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff566372)イベント。 サイズ、**れた WNODE\_* XXX*** と変数のデータは、レジストリで定義された制限の 1 K を超えることはできません。

2. すべてのメンバーを初期化します、**れた WNODE\_* XXX*** 構造体を含む**WnodeHeader.Flags**:

   - ドライバーのセット、**れた WNODE\_フラグ\_イベント\_項目**構造がイベントであることを示すフラグ。

   - ドライバーの設定の種類を示す次のフラグのいずれかの**れた WNODE\_* XXX*** 構造体。

     **WNODE\_FLAG\_ALL\_DATA**

     **れた WNODE\_フラグ\_単一\_インスタンス**

     **れた WNODE\_フラグ\_単一\_項目**

   - ドライバーを設定またはブロックが静的または動的なインスタンス名を使用するかどうかを示す次のフラグをクリアします。

     **WNODE\_FLAG\_STATIC\_INSTANCE\_NAMES**

     **れた WNODE\_フラグ\_PDO\_インスタンス\_名**

   - ドライバーは、イベントに応じて追加のフラグを設定します。

3. ポインターをキャスト、**れた WNODE\_* XXX***、PWNODE に\_イベント\_項目。

4. 呼び出し**IoWMIWriteEvent**ポインター。

   場合**IoWMIWriteEvent**イベントの WMI リリース ドライバーに割り当てられたメモリが正常に完了します。

後[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520) 、ドライバーは、イベントのトリガーの条件を監視して、WMI を送信するまで、そのトリガーの条件が発生するたびに、イベントの送信が再開されますを返します、 [ 。**IRP\_MN\_を無効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550851)そのイベントを無効にする要求。

イベントのサイズがレジストリ定義の最大数を超えた場合、ドライバーを呼び出す必要があります (非推奨) 1 K の**IoWmiWriteEvent**初期化された[**れた WNODE\_イベント\_参照**](https://msdn.microsoft.com/library/windows/hardware/ff566374)イベントの GUID、サイズ、およびその (静的なインスタンス名) のインスタンスのインデックスまたは (動的なインスタンス名) の名前を指定します。 WMI が内の情報を使用して、**れた WNODE\_イベント\_参照**イベントを照会します。

ドライバーは、動的なインスタンス名を使用しないイベントを送信して、1 つのインスタンスの WMI のライブラリ ルーチンを呼び出すことによって構成される[ **WmiFireEvent**](https://msdn.microsoft.com/library/windows/hardware/ff565807)します。 ドライバーは、割り当て、初期化する必要はありません、**れた WNODE\_* XXX*** 用の構造を**WmiFireEvent**呼び出します。 WMI でドライバーのイベント データをパッケージ化、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)データ コンシューマーに配信します。 イベントを送信の詳細については**WmiFireEvent**を参照してください[WmiFireEvent でイベントを送信する](sending-an-event-with-wmifireevent.md)します。

 

 




