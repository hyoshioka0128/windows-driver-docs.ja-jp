---
title: サード パーティ製フィルター ドライバー
ms.assetid: 2EAFE726-2266-4E40-AC51-0025BF6069B6
description: サンプルのフィルター ドライバーで、Microsoft Windows Driver Kit (WDK)。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 763eb9aa7503a66938bdee9dddefde5e806c5cf1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538815"
---
# <a name="3rd-party-filter-drivers"></a>サード パーティ製フィルター ドライバー


このトピックでは、次のサンプル フィルター ドライバーの Microsoft Windows Driver Kit (WDK) の機能について説明します。

-   **Kbfiltr**、プラグ アンド プレイ PS/2 スタイル キーボード デバイス用の省略可能な上位レベルのフィルター ドライバー

-   **Moufiltr**、プラグ アンド プレイ スタイル 2 PS/マウス デバイス用の省略可能な上位レベルのフィルター ドライバー

Kbfiltr と Moufiltr、I/O 要求をフィルター処理し、クラスのサービスの操作と I8042prt の操作を変更するコールバック ルーチンを追加する方法を説明します。

**注**  以降 Windows 2000 のターミナル サーバーのデザインは、リモート クライアントに物理的にインストールされているデバイスからの入力をフィルター処理するサンプルのキーボードとマウスのフィルター ドライバーを使用してをサポートしていません。 ターミナル サーバーにインストールされているフィルター ドライバーは、ターミナル サーバーに物理的にインストールされているデバイスからの入力をフィルター処理にのみ使用できます。 これは、ターミナル サーバーの TermDD.sys ドライバーがリモート クライアントからの入力を処理する方法の結果です。

 

Kbfiltr と Moufiltr プラグ アンド プレイし、電源管理をサポートします。

Kbfiltr には、次のコールバック ルーチンが用意されています。

<a href="" id="kbfilter-servicecallback"></a>[**KbFilter\_ServiceCallback**](https://msdn.microsoft.com/library/windows/hardware/ff542297)  
キーボードのフィルター サービスのコールバックは、キーボード クラスのサービスのコールバックに追加されます。 クラス ドライバーのデータのキューに保存されているキーボード入力データを変更するのには、フィルター サービスのコールバックを構成できます。

<a href="" id="kbfilter-isrhook"></a>[**KbFilter\_IsrHook**](https://msdn.microsoft.com/library/windows/hardware/ff542294)  
キーボード フィルター ISR フック ルーチンが用のテンプレート、 **IsrRoutine** I8042prt キーボード デバイスをサポートするコールバック。 キーボードの ISR の操作をカスタマイズするコールバックを構成できます。

<a href="" id="kbfilter-initializationroutine"></a>[**KbFilter\_InitializationRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff542293)  
キーボードのフィルターの初期化ルーチンは、テンプレート、 **InitializationRoutine** I8042prt キーボード デバイスをサポートするコールバック。 キーボード デバイスの初期化をカスタマイズするのには、このコールバックを構成できます。

Moufiltr には、次のコールバック ルーチンが用意されています。

<a href="" id="moufilter-servicecallback"></a>[**MouFilter\_ServiceCallback**](https://msdn.microsoft.com/library/windows/hardware/ff542380)  
マウス フィルター サービスのコールバックは、マウス クラスのサービスのコールバックに追加されます。 クラス ドライバーのデータのキューに保存されているマウス入力データを変更するのには、フィルター サービスのコールバックを構成できます。

<a href="" id="moufilter-isrhook"></a>[**MouFilter\_IsrHook**](https://msdn.microsoft.com/library/windows/hardware/ff542379)  
マウス フィルター ISR フック ルーチンが用のテンプレート、 **IsrRoutine** I8042prt マウス デバイスをサポートするコールバック。 コールバックは、ネズミの ISR. の操作をカスタマイズするように構成できます。

## <a name="customize-the-initialization-and-isr-of-a-device"></a>初期化と ISR デバイスをカスタマイズします。


ベンダーは、I8042prt の操作には、次の省略可能なコールバックを追加できるオプションの上位レベルのデバイスのフィルター ドライバーを指定できます。

<a href="" id="pi8042-keyboard-isr"></a>[**PI8042\_キーボード\_ISR**](https://msdn.microsoft.com/library/windows/hardware/ff543248)  
キーボードの割り込みサービス ルーチン (ISR) ISR. I8042prt キーボードの操作をカスタマイズします。 I8042prt の既定の操作のための十分な場合は、キーボードの ISR コールバックは必要ありません。 I8042prt キーボード ISR がキーボードの割り込みを検証した後、キーボードの ISR コールバックを呼び出します。

<a href="" id="pi8042-mouse-isr"></a>[**PI8042\_マウス\_ISR**](https://msdn.microsoft.com/library/windows/hardware/ff543252)  
マウス ISR ISR. I8042prt マウスの操作をカスタマイズします。 I8042prt の既定の操作のための十分な場合は、マウスの ISR コールバックは必要ありません。 I8042prt マウス ISR がマウスの割り込みを検証した後は、マウスの ISR コールバックを呼び出します。

<a href="" id="pi8042-keyboard-initialization-routine"></a>[**PI8042\_キーボード\_初期化\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff543243)  
キーボードの初期化のコールバックは、I8042prt によってキーボード デバイスの既定の初期化を補足します。 I8042prt は、キーボード デバイスを初期化するときに、このルーチンを呼び出します。

I8042prt を使用して、上位レベルのデバイスのフィルター ドライバーによって提供されるコールバックを追加する、 [ **IOCTL\_内部\_I8042\_フック\_キーボード**](https://msdn.microsoft.com/library/windows/hardware/ff541233)キーボード デバイスの要求と[ **IOCTL\_内部\_I8042\_フック\_マウス**](https://msdn.microsoft.com/library/windows/hardware/ff541242)マウス デバイスを要求します。 I8042prt クラスのデバイス ドライバーからの接続要求を受け取った後 I8042prt は同期的に、デバイス スタックの先頭に、デバイスに固有のフック要求を送信します。

フィルター ドライバーは、フック要求を受信した後、次は。

-   あるフィルター ドライバーに渡される場合にフックについては、上位レベルのドライバーを保存します。

    フック情報には、コンテキストへのポインターには、ISR コールバックへのポインターには初期化のコールバック (キーボードの場合のみ初期化コールバック) へのポインターが含まれます。

-   上位レベルのドライバー用のフックの情報をフィルター ドライバーのフック情報に置き換えます。

-   フィルター ドライバーのコールバックを使用するコールバックを I8042prt と、ポインターのコンテキストを保存します。

Kbfiltr と Moufiltr、サンプル フィルター ドライバーは、次のコールバック ルーチンを提供します。

-   [**KbFilter\_IsrHook** ](https://msdn.microsoft.com/library/windows/hardware/ff542294) 、PI8042 のテンプレートは、\_キーボード\_ISR コールバック。

-   [**KbFilter\_InitializationRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff542293) 、PI8042 のテンプレートは、\_キーボード\_初期化\_ルーチンのコールバック。

-   [**MouFilter\_IsrHook** ](https://msdn.microsoft.com/library/windows/hardware/ff542379) 、PI8042 のテンプレートは、\_マウス\_ISR コールバック。

## <a name="synchronize-the-operation-of-a-filter-driver-with-a-devices-isr"></a>デバイスの ISR とフィルター ドライバーの操作を同期します。


I8042prt は、そのデバイス スタックの上位レベルのドライバーにデバイスの割り込みのオブジェクトへのポインターを渡すための開始情報の要求を使用します。 デバイスが開始されると、フィルター ドライバーは、割り込みサービス ルーチンとその操作を同期するのに割り込みオブジェクトを使用できます。 フィルター ドライバーの呼び出しで割り込みオブジェクトを使用する必要がありますのみ[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)します。

使用して、デバイス スタックの先頭に割り込みオブジェクトへのポインターを渡します I8042prt、 [ **IOCTL\_内部\_I8042\_キーボード\_開始\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541257)キーボード デバイスの要求と[ **IOCTL\_内部\_I8042\_マウス\_開始\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541265)マウス デバイスを要求します。 I8042prt は同期的に、デバイスのハードウェアの初期化後に、デバイス スタックの上部に開始情報の要求を送信します。 フィルター ドライバーは開始情報の要求を受信後開始情報を保存し、デバイス スタックの要求を渡します。 I8042prt では、要求を完了します。

## <a name="synchronize-writes-by-a-filter-driver-to-a-device"></a>デバイス フィルター ドライバーでの同期書き込み


デバイスの操作をカスタマイズするには、フィルター ドライバーは、デバイスにコントロールのデータを書き込む必要があります。 フィルター ドライバーは、デバイスの割り込みサービス ルーチンとデバイスへの書き込みを同期する必要があり、その他の非同期の読み取りまたはデバイス (たとえば、set 続けた要求またはセット キーボードのインジケーターの要求によって開始された書き込み) に書き込みます。

I8042prt サポート、 [ **IOCTL\_内部\_I8042\_キーボード\_書き込み\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff541263)要求と[**IOCTL\_内部\_I8042\_マウス\_書き込み\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff541270)この目的のための要求。 書き込みバッファーの要求は、デバイスの ISR とデバイスの読み取りまたはその他の要求と同期されます。

## <a name="i8042prt-callbacks-that-filter-drivers-can-use"></a>フィルター ドライバー I8042prt コールバックを使用できます。


I8042prt は、その ISR コールバックで、上位レベルのデバイスのフィルター ドライバーを使用して次のコールバックをサポートします。

<a href="" id="pi8042-isr-write-port"></a>[**PI8042\_ISR\_書き込み\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff543231)  
デバイスの書き込みポート コールバックは、デバイスの ISR. の IRQL で i8042 ポートに書き込みます

<a href="" id="pi8042-queue-packet"></a>[**PI8042\_キュー\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff543263)  
デバイスのキュー パケットのコールバックは、デバイスの ISR で処理するため、入力データ パケットをキュー *DPC*します。

<a href="" id="pi8042-synch-read-port"></a>[**PI8042\_同期\_読み取り\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff543272)  
このコールバックで使用できる、 [ **PI8042\_キーボード\_初期化\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff543243)コールバック。 I8042prt で読み取りのポートのコールバックを指定します、*して*パラメーターその I8042prt がキーボードの初期化ルーチンを入力します。

<a href="" id="pi8042-synch-write-port"></a>[**PI8042\_同期\_書き込み\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff543276)  
このコールバックで使用できる、 [ **PI8042\_キーボード\_初期化\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff543243)コールバック。 I8042prt がで書き込みポートのコールバックを指定します、 *WritePort*パラメーターその I8042prt がキーボードの初期化ルーチンを入力します。

キーボード デバイス コールバックに I8042prt がポインターを渡す、 [**内部\_I8042\_フック\_キーボード**](https://msdn.microsoft.com/library/windows/hardware/ff541039) I8042prt を使用して情報を入力する構造体[ **IOCTL\_内部\_I8042\_フック\_キーボード**](https://msdn.microsoft.com/library/windows/hardware/ff541233)要求。

マウス デバイス コールバックを I8042prt がポインターを渡す、 [**内部\_I8042\_フック\_マウス**](https://msdn.microsoft.com/library/windows/hardware/ff541044) I8042prt を使用して情報を入力する構造体、[ **IOCTL\_内部\_I8042\_フック\_キーボード**](https://msdn.microsoft.com/library/windows/hardware/ff541233)要求。

フィルター ドライバーは、フック デバイス要求を受信した後、フィルター ドライバーの ISR コールバックで使用するための I8042prt コールバック ポインターを保存します。

 

 




