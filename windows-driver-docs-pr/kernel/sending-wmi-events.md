---
title: WMI イベントの送信
description: WMI イベントの送信
ms.assetid: 0d5e62f1-b84e-42b7-be40-8665f0b58ba8
keywords:
- WMI の WDK カーネルでは、イベントの追跡
- WDK の WMI イベント
- WDK の WMI のトレース
- WMI イベントの送信
- イベントは、WDK の WMI をブロックします。
- WDK の WMI の通知
- WDK の WMI の名前の動的インスタンス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c08a40310671c2f49f3b48326c82738b06774a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539117"
---
# <a name="sending-wmi-events"></a>WMI イベントの送信





ドライバーは、アプリケーションに通知するユーザー モード イベントのポーリング、Irp を送信するのにアプリケーションを必要とせず、WMI イベントを使用できます。 ドライバーは、WMI イベントを使用して、エラーのログ記録の代替としてではなく、例外的な条件の WMI クライアントに通知する必要があります。 ドライバーする必要があります Wmicore.mof でそのデバイスの種類に対して定義されているすべての標準的なイベント ブロックをサポートし、可能性がありますを定義および登録デバイスに固有の通知をサポートする追加のカスタム イベント ブロック。

イベント ブロックは、抽象基本クラスから派生したデータ ブロックだけ**WMIEvent**します。 イベント ブロックは、データ ブロックとして、同じデータのいずれかを含めることができます、または空にすること、つまり、イベント ブロックには必要がありますが含まれていないドライバーの定義済みのデータ項目には。 イベント ブロックには、データ合計サイズにはが含まれてかどうか、**れた WNODE\_* XXX*** に加えて、データは 1 キロバイトのレジストリで定義されている制限を超えることはできません。 一般に、システム パフォーマンスが向上しよりタイムリーな通知の小さいイベントが発生します。 ブロックを定義する方法の詳細については、[WMI データとイベント ブロックの MOF 構文](mof-syntax-for-wmi-data-and-event-blocks.md)と[WMI データの設計とイベント ブロック](designing-wmi-data-and-event-blocks.md)を参照してください。

ドライバーが WMIREG に対応するイベント ブロックを登録すると、イベントのサポートを示す\_フラグ\_イベント\_のみ\_GUID が、ブロックの設定[ **WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)構造体。 ブロックを登録する方法の詳細については、[WMI データ プロバイダーとして登録する](registering-as-a-wmi-data-provider.md)を参照してください。

WMI クライアント ユーザーが、イベントの通知を要求時に WMI を送信する[ **IRP\_MN\_を有効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550859)するアラート、ドライバーを開始すると、ドライバーへの要求イベントのドライバーにより決定されたトリガーの条件を監視します。 次に、トリガーの条件が発生したときに、ドライバーは WMI で、イベントが登録されているすべてのデータ コンシューマーに配信するイベントを送信します。

ドライバーは、次の方法のいずれかで wmi イベントを送信します。

- カーネル モードの WMI ライブラリ ルーチンを呼び出す[ **WmiFireEvent**](https://msdn.microsoft.com/library/windows/hardware/ff565807)します。 ドライバーが呼び出せる**WmiFireEvent**動的インスタンスの名前を使用しないし、1 つのベース名の文字列または PDO のデバイス インスタンス ID を静的インスタンス名を基にのみイベントを送信します。 さらに、イベントが 1 つのインスタンスをする必要があります: ドライバーを呼び出すことはできません、 **WmiFireEvent**の 1 つまたは複数のインスタンスで構成されるイベントを送信します。 詳細については、[WmiFireEvent でイベントを送信する](sending-an-event-with-wmifireevent.md)を参照してください。

- カーネル モードのルーチンを呼び出す[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)ドライバーに割り当てられたへのポインターを初期化および**れた WNODE\_* XXX*** 構造体を含む、イベントのデータ。 詳細については、[IoWMIWriteEvent でイベントを送信する](sending-an-event-with-iowmiwriteevent.md)を参照してください。

 

 




