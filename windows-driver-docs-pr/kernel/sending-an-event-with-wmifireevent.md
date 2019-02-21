---
title: WmiFireEvent でイベントを送信します。
description: WmiFireEvent でイベントを送信します。
ms.assetid: f9cf8491-0f5a-4d83-849f-3edb77488092
keywords:
- WMI の WDK カーネルでは、イベントの追跡
- WDK の WMI イベント
- WDK の WMI のトレース
- WMI イベントの送信
- イベントは、WDK の WMI をブロックします。
- WDK の WMI の通知
- WmiFireEvent
- WDK の WMI の名前の動的インスタンス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd6ae6b9dda93810b374e1160a852fde64ffd8d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550499"
---
# <a name="sending-an-event-with-wmifireevent"></a>WmiFireEvent でイベントを送信します。





ドライバーが呼び出せる[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)動的インスタンスの名前を使用しないし、1 つのベース名の文字列または PDO のデバイス インスタンス ID を静的インスタンス名を基にイベントを送信します。

イベントは、ブロックの 1 つのインスタンスである必要があります: ドライバーを呼び出すことはできません、 **WmiFireEvent**の 1 つまたは複数のインスタンスで構成されるイベントを送信します。 このようなイベントを送信するドライバーを呼び出す必要があります[ **IoWMIWriteEvent**](https://msdn.microsoft.com/library/windows/hardware/ff550520)」の説明に従って、 [IoWMIWriteEvent でイベントを送信する](sending-an-event-with-iowmiwriteevent.md)します。

ドライバーは、WMI がイベントを有効になるまでのイベントを送信しないでください。 イベントを有効になっている場合、イベントのトリガー条件が発生したドライバー。

1.  非ページ プールからバッファーを割り当て、イベント データをバッファーに書き込みます。 イベントにデータがあるない場合、ドライバーは、この手順を省略できます。

2.  呼び出し[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)は次のパラメーター。

    -   ドライバーのデバイス オブジェクトへのポインター

    -   イベント ブロックを表す GUID へのポインター

    -   イベント ブロックに複数のインスタンス、インスタンスのインデックスがある場合

    -   データが送信されるイベント、データのバイト数または 0 の場合に none の場合

    -   データが、データを格納しているドライバーによって割り当てられたバッファーへのポインター、イベントと共に送信される場合または**NULL**なしの場合

    ドライバーに渡されるすべてのパラメーターを割り当てる必要があります**WmiFireEvent**、非ページ プールから、イベントのデータ バッファーを含むです。 WMI は、ドライバーによって、操作を行うドライバーに割り当てられたメモリを解放します。

後**WmiFireEvent**返します、ドライバーは、イベントのトリガーの条件の監視を再開し、WMI は、そのイベントを無効にするまで、そのトリガーの条件が発生するたびにイベントを送信します。

 

 




