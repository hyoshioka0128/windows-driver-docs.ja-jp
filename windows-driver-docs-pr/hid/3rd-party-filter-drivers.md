---
title: サード パーティのフィルター ドライバー
ms.assetid: 2EAFE726-2266-4E40-AC51-0025BF6069B6
description: Microsoft Windows Driver Kit (WDK) のサンプルフィルタードライバー。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044843853336f840c598371c5fd156c63be0288e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824884"
---
# <a name="3rd-party-filter-drivers"></a>サード パーティのフィルター ドライバー


このトピックでは、Microsoft Windows Driver Kit (WDK) の次のサンプルフィルタードライバーの機能について説明します。

-   **Kbfiltr**(プラグアンドプレイ PS/2 スタイルのキーボードデバイス用のオプションの上位レベルフィルタードライバー)

-   プラグアンドプレイ PS/2 スタイルのマウスデバイス用のオプションの上位レベルフィルタードライバーである、フォント**tr**

Kbfiltr と I8042prt Filtr は、i/o 要求をフィルター処理し、クラスサービスとその操作を変更するコールバックルーチンを追加する方法を示しています。

**注**   Windows 2000 以降のターミナルサーバーの設計では、リモートクライアントに物理的にインストールされているデバイスからの入力をフィルター処理するためのサンプルキーボードおよびマウスフィルタードライバーの使用はサポートされていません。 ターミナルサーバーにインストールされているフィルタードライバーは、ターミナルサーバーに物理的にインストールされているデバイスからの入力をフィルター処理するためにのみ使用できます。 これは、ターミナルサーバーの Termdd.sys ドライバーがリモートクライアントからの入力を処理する方法の結果です。

 

Kbfiltr およびの機能は、プラグアンドプレイと電源管理をサポートしています。

Kbfiltr には、次のコールバックルーチンが用意されています。

<a href="" id="kbfilter-servicecallback"></a>[**KbFilter\_ServiceCallback**](https://docs.microsoft.com/previous-versions/ff542297(v=vs.85))  
キーボードフィルターサービスのコールバックが、キーボードクラスのサービスコールバックに追加されます。 フィルターサービスのコールバックは、クラスドライバーのデータキューに保存されているキーボード入力データを変更するように構成できます。

<a href="" id="kbfilter-isrhook"></a>[**KbFilter\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542294(v=vs.85))  
キーボードフィルター ISR フックルーチンは、I8042prt がキーボードデバイスに対してサポートする**Isrroutine**コールバックのテンプレートです。 コールバックは、キーボードの ISR の操作をカスタマイズするように構成できます。

<a href="" id="kbfilter-initializationroutine"></a>[**KbFilter\_InitializationRoutine**](https://docs.microsoft.com/previous-versions/ff542293(v=vs.85))  
キーボードフィルター初期化ルーチンは、I8042prt がキーボードデバイスをサポートする**InitializationRoutine**コールバックのテンプレートです。 このコールバックは、キーボードデバイスの初期化をカスタマイズするように構成できます。

の機能には、次のコールバックルーチンが用意されています。

<a href="" id="moufilter-servicecallback"></a>[**ServiceCallback フィルター\_** ](https://docs.microsoft.com/previous-versions/ff542380(v=vs.85))  
マウスフィルターサービスのコールバックがマウスクラスのサービスコールバックに追加されます。 フィルターサービスのコールバックは、クラスドライバーのデータキューに保存されているマウス入力データを変更するように構成できます。

<a href="" id="moufilter-isrhook"></a>[ **\_IsrHook の場合は、このフィルター**](https://docs.microsoft.com/previous-versions/ff542379(v=vs.85))  
マウスフィルター ISR フックルーチンは、I8042prt がマウスデバイスに対してサポートする**Isrroutine**コールバックのテンプレートです。 コールバックは、そのマウスの ISR の操作をカスタマイズするように構成できます。

## <a name="customize-the-initialization-and-isr-of-a-device"></a>デバイスの初期化と ISR をカスタマイズする


ベンダーは、次のオプションのコールバックを I8042prt の操作に追加できる、オプションの上位レベルのデバイスフィルタードライバーを提供できます。

<a href="" id="pi8042-keyboard-isr"></a>[**PI8042\_キーボード\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_isr)  
キーボード割り込みサービスルーチン (ISR) は、I8042prt キーボード ISR の操作をカスタマイズします。 I8042prt の既定の操作で十分であれば、キーボード ISR コールバックは必要ありません。 I8042prt キーボード ISR は、キーボードの割り込みを検証した後、キーボード ISR コールバックを呼び出します。

<a href="" id="pi8042-mouse-isr"></a>[**PI8042\_マウス\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_mouse_isr)  
マウス ISR は、I8042prt マウス ISR の操作をカスタマイズします。 I8042prt の既定の操作で十分であれば、マウス ISR コールバックは必要ありません。 I8042prt マウス ISR はマウスの割り込みを検証した後、マウスの ISR コールバックを呼び出します。

<a href="" id="pi8042-keyboard-initialization-routine"></a>[**PI8042\_キーボード\_初期化\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)  
キーボード初期化コールバックでは、I8042prt によるキーボードデバイスの既定の初期化が補完されます。 I8042prt は、キーボードデバイスを初期化するときにこのルーチンを呼び出します。

I8042prt[**内部\_i8042\_フック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)を使用して、上位レベルのデバイスフィルタードライバーによって提供されるコールバックを追加します。これには、キーボードデバイスと[**ioctl\_内部\_I8042 の\_キーボード要求を\_@no__t**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_mouse)マウスデバイスに対するマウス要求をフック\_する (_s) I8042prt がデバイスクラスドライバーから connect 要求を受信すると、I8042prt はデバイス固有のフック要求をデバイススタックの一番上に同期的に送信します。

フィルタードライバーは、フック要求を受け取った後、次の処理を実行します。

-   フィルタードライバーに渡される上位レベルのドライバーのフック情報がある場合は、それを保存します。

    フック情報には、コンテキストへのポインター、ISR コールバックへのポインター、および初期化コールバックへのポインター (キーボードのみの初期化コールバック) が含まれます。

-   上位レベルのドライバーのフック情報をフィルタードライバーのフック情報に置き換えます。

-   I8042prt のコンテキストと、フィルタードライバーのコールバックが使用できるコールバックへのポインターを保存します。

サンプルのフィルタードライバーである Kbfiltr とには、次のコールバックルーチンが用意されています。

-   [**Kbfilter\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542294(v=vs.85))は、PI8042\_キーボード\_ISR コールバックのテンプレートです。

-   [**Kbfilter\_InitializationRoutine**](https://docs.microsoft.com/previous-versions/ff542293(v=vs.85))は、PI8042\_キーボード\_初期化\_ルーチンコールバックのテンプレートです。

-   [ **\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542379(v=vs.85))は、PI8042\_MOUSE\_ISR コールバックのテンプレートです。

## <a name="synchronize-the-operation-of-a-filter-driver-with-a-devices-isr"></a>フィルタードライバーの操作をデバイスの ISR と同期させる


I8042prt は、開始情報要求を使用して、デバイスの割り込みオブジェクトへのポインターを、デバイススタック内の上位レベルのドライバーに渡します。 デバイスが起動した後、フィルタードライバーは interrupt オブジェクトを使用して、割り込みサービスルーチンとその操作を同期できます。 フィルタードライバーは、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)の呼び出しでのみ、interrupt オブジェクトを使用する必要があります。

I8042prt は、 [**ioctl\_内部\_I8042\_キーボード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_start_information)を使用して、割り込みオブジェクトポインターをデバイススタックの一番上に渡します。これは、キーボードデバイスの\_情報要求を開始\_、 [**ioctl\_内部\_I8042\_マウス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_start_information)マウスデバイスの\_情報の要求を開始します。 I8042prt は、デバイスのハードウェアの初期化後に、デバイススタックの最上位に開始情報要求を同期的に送信します。 フィルタードライバーは、開始情報要求を受信した後、開始情報を保存し、デバイススタックに要求を渡します。 I8042prt は要求を完了します。

## <a name="synchronize-writes-by-a-filter-driver-to-a-device"></a>フィルタードライバーによる書き込みをデバイスに同期する


デバイスの操作をカスタマイズするには、フィルタードライバーがデバイスに制御データを書き込む必要があります。 フィルタードライバーは、デバイスへの書き込みをデバイスに同期させる必要があります (たとえば、set 速度要求またはキーボードインジケーターの設定要求によって開始される書き込みなど)。

I8042prt は、[**内部\_i8042\_\_キーボード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_write_buffer)を使用して、\_バッファー要求を書き込み、 [**ioctl\_内部\_i8042\_マウス\_\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_write_buffer)要求を書き込むことができる ioctl\_をサポートしています。この目的は次のようになります。 書き込みバッファー要求は、デバイスの ISR と、デバイスの読み取りまたは書き込みを行う他の要求と同期されます。

## <a name="i8042prt-callbacks-that-filter-drivers-can-use"></a>フィルタードライバーが使用できる I8042prt コールバック


I8042prt は、上位レベルのデバイスフィルタードライバーが ISR コールバックで使用できる次のコールバックをサポートしています。

<a href="" id="pi8042-isr-write-port"></a>[**PI8042\_ISR\_書き込み\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_isr_write_port)  
デバイスの書き込みポートコールバックは、デバイスの ISR の IRQL で、i8042 ポートに書き込みます。

<a href="" id="pi8042-queue-packet"></a>[**PI8042\_QUEUE\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_queue_packet)  
デバイスのキューパケットコールバックは、デバイスの ISR *DPC*によって処理するために入力データパケットをキューに置いています。

<a href="" id="pi8042-synch-read-port"></a>[**PI8042\_同期\_\_ポートの読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_synch_read_port)  
このコールバックは、 [**PI8042\_のキーボード\_初期化\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)コールバックで使用できます。 I8042prt は、キーボード初期化ルーチンへの入力を I8042prt する*readport*パラメーターの読み取りポートコールバックを指定します。

<a href="" id="pi8042-synch-write-port"></a>[**PI8042\_同期\_書き込み\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_synch_write_port)  
このコールバックは、 [**PI8042\_のキーボード\_初期化\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)コールバックで使用できます。 I8042prt は、キーボード初期化ルーチンへの入力を I8042prt する*writeport*パラメーターの書き込みポートコールバックを指定します。

I8042prt は、[**内部\_i8042\_フック\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ns-ntdd8042-_internal_i8042_hook_keyboard)のキーボードデバイスコールバックへのポインターを渡します。この構造体は、I8042prt が[**IOCTL\_内部\_I8042\_フックを使用して情報を入力するために使用し\_キーボード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)要求。

I8042prt は、I8042prt が内部\_I8042\_フックを使用し\_て情報を入力するために使用する、[**内部\_i8042\_フック\_の**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ns-ntdd8042-_internal_i8042_hook_mouse)のマウスデバイスコールバックへのポインターを渡し[ **\_キーボード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)要求。

フィルタードライバーは、フックデバイスの要求を受け取った後、フィルタードライバーの ISR コールバックで使用する I8042prt コールバックポインターを保存します。

 

 




