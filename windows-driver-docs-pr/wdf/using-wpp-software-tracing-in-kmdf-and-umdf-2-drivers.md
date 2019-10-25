---
title: KMDF および UMDF 2 ドライバーでのインフライト トレース レコーダー (IFR) の使用
description: Windows 10 以降では、WDF ドライバーをビルドして、Windows ソフトウェアトレース前処理を通じて追加のドライバーデバッグ情報を取得できるようにすることができます。
ms.assetid: CA2A7ED3-4372-4EE9-8B04-042A8C864BD5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ff3a3efe27d986c2cb70c520271f01fee44021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845423"
---
# <a name="using-inflight-trace-recorder-ifr-in-kmdf-and-umdf-2-drivers"></a>KMDF および UMDF 2 ドライバーでのインフライト トレース レコーダー (IFR) の使用


Windows 10 以降では、Windows ソフトウェアトレース前処理を通じて追加のドライバーデバッグ情報を取得できるように、KMDF または UMDF ドライバーをビルドできます。 この機能は、Inflight トレースレコーダー (IFR) と呼ばれ、KMDF バージョン1.15 および UMDF バージョン2.15 以降で使用できます。

Inflight トレースレコーダーは、 [WPP ソフトウェアトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)の拡張機能です。 WPP トレースとは異なり、Inflight トレースレコーダーは、アタッチされたトレースコンシューマーなしで引き続き動作します。 フレームワークは、メッセージを循環バッファーに書き込みます。また、ドライバーは独自のメッセージを追加することもできます。 各ドライバーには独自のログがあるため、ドライバーに関連付けられている複数のデバイスが1つのログを共有します。

ログは、ページング不可能なメモリに格納されるので、システムのクラッシュ後に復旧できます。 また、Inflight トレースレコーダーのログはミニダンプファイルにも含まれています。

**Inflight トレースレコーダーを有効にし、ドライバーからメッセージを送信する方法**

1.  Microsoft Visual Studio で、次の操作を行います。

    -   ドライバープロジェクトのプロパティページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。 ドライバーのプロパティページで、 **[構成プロパティ]** 、 **[Wpp トレース]** の順にクリックします。 **[全般]** メニューの [ **WPP トレース**の実行 **] を [はい]** に設定します。

    -   **プロパティ-&gt;Wpp トレース-&gt;関数およびマクロオプション** に移動し、**Wpp レコーダーを有効にする** を選択します。

    -   同じメニューで、 **Scan Configuration Data**をトレース情報を含むファイル (たとえば、trace. h) に設定します。

2.  WPP マクロを呼び出す各ソースファイルで、[トレースメッセージヘッダー (TMH) ファイル](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)を識別する **\#include**ディレクティブを追加します。 ファイル名は、&lt;の形式である必要があります *。ファイル名*&gt; **。**

    たとえば、ドライバーが*MyDriver1*と*MyDriver2*という2つのソースファイルで構成されている場合、 *MyDriver1*には次のものが含まれている必要があります。

    **"MyDriver1" を含めるには\#**

    および*MyDriver2*には次のものが含まれている必要があります。

    **"MyDriver2" を含めるには\#**

    Visual Studio でドライバーをビルドすると、WPP プリプロセッサによってが生成されます。*tmh*ファイル。

3.  ヘッダーファイルで、 [WPP\_制御\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロを定義します。 このマクロは、ドライバーのトレースメッセージの GUID と[トレースフラグ](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)を定義します。

    Osrusbfx2 driver サンプルでは、次の例に示すように、Trace ヘッダーファイルに1つのコントロール GUID と7つのトレースフラグを定義します。

    ```cpp
    #define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(OsrUsbFxTraceGuid, \
      (d23a0c5a,d307,4f0e,ae8e,E2A355AD5DAB), \
      WPP_DEFINE_BIT(DBG_INIT)          /* bit  0 = 0x00000001 */ \
      WPP_DEFINE_BIT(DBG_PNP)           /* bit  1 = 0x00000002 */ \
      WPP_DEFINE_BIT(DBG_POWER)         /* bit  2 = 0x00000004 */ \
      WPP_DEFINE_BIT(DBG_WMI)           /* bit  3 = 0x00000008 */ \
      WPP_DEFINE_BIT(DBG_CREATE_CLOSE)  /* bit  4 = 0x00000010 */ \
      WPP_DEFINE_BIT(DBG_IOCTL)         /* bit  5 = 0x00000020 */ \
      WPP_DEFINE_BIT(DBG_WRITE)         /* bit  6 = 0x00000040 */ \
      WPP_DEFINE_BIT(DBG_READ)          /* bit  7 = 0x00000080 */ \
    )
    ```

    この例では、次の操作を行います。

    -   **Osrusbfxtraceguid**は {D23A0C5A-D307-4F0E-AE8E-E2A355AD5DAB} GUID のフレンドリ名です。
    -   トレースフラグは、ドライバーがさまざまな種類の i/o 要求を処理するときに生成されるトレースメッセージを区別するために使用されます。

4.  ドライバー (KMDF と UMDF 2 の両方) は、ドライバーオブジェクトとレジストリパス (通常は[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)) を使用して、[**カーネルモードドライバー用の WPP\_INIT\_トレースを**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556193(v=vs.85))呼び出す必要があります。

    ```cpp
    WPP_INIT_TRACING( DriverObject, RegistryPath );
    ```

    トレースを非アクティブ化するには、KMDF と UMDF 2 の両方のドライバーが、 [*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)または[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)から[**カーネルモードドライバーの\_クリーンアップ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556183(v=vs.85))を呼び出します。

    ```cpp
    WPP_CLEANUP( WdfDriverWdmGetDriverObject( Driver ));
    ```

    [**WPP\_クリーンアップ**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556183(v=vs.85))マクロは pdriver\_OBJECT 型のパラメーターを受け取ります。そのため、ドライバー[**の driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)が失敗した場合は、 [**Wdfdriverwdmgetdriverobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverwdmgetdriverobject)の呼び出しをスキップし、代わりにを使用して**wpp\_クリーンアップ**を呼び出すことができます。WDM ドライバーオブジェクトへのポインター。

    UMDF バージョン2.15 以降では、UMDF ドライバーは、これらのマクロのカーネルモード署名を使用して、トレースを初期化およびクリーンアップします。 これは、KMDF と UMDF の呼び出しが同じであることを意味します。

5.  トレースメッセージを作成するには、ドライバーで[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロまたはマクロのカスタマイズされた[バージョン](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)を使用します。

    次の例では、読み取り要求の処理に使用するコードの一部で、Osrusbfx2 ドライバーが**Traceevents**関数を使用する方法を示しています。

    ```cpp
    if (Length > TEST_BOARD_TRANSFER_BUFFER_SIZE) {
        TraceEvents(TRACE_LEVEL_ERROR,
                    DBG_READ,
                    "Transfer exceeds %d\n",
                    TEST_BOARD_TRANSFER_BUFFER_SIZE);
     
        status = STATUS_INVALID_PARAMETER;
    }
    ```

    トレースコントローラーでトレース **\_レベル\_エラー**レベルと**DBG\_READ**トレースフラグが有効になっている場合、 **traceevents**を呼び出すと、トレースメッセージが生成されます。 このメッセージには、ドライバーによって定義された定数**テスト\_ボード\_転送\_バッファー\_サイズ**の値が含まれます。

6.  ドライバーログで使用される循環バッファーのサイズを変更するには、次のレジストリの場所にある**Logpages**レジストリ値を変更します。

    <a href="" id="for-umdf-"></a>UMDF の場合:  

    **ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;ドライバー&gt;\\パラメーター\\Wdf**

    <a href="" id="for-kmdf-"></a>KMDF の場合:  

    **HKEY\_ローカル\_マシン\\System\\CurrentControlSet\\Services\\&lt;ドライバー&gt;\\パラメーター\\Wdf**

    これは、ページに割り当てられたログバッファーのサイズを格納する**REG\_DWORD**型の値です。 有効な値は、0x1 ~ 0x10 です。

**KMDF ドライバーの場合**

1.  デバッガーに「 **load rcdrkd .dll** 」と入力して、rcdrkd コマンドを読み込みます。
2.  Windows ドライバーフレームワーク (WDF) に現在動的にバインドされているドライバーに関する情報を表示するには、 [ **! wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)拡張機能を使用します。
3.  ドライバーによって提供されるメッセージを表示するには、 [ **! rcdrkd. rcdrlogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-rcdrkd-rcdrlogdump)および[ **! rcdrkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-rcdrkd-rcdrcrashdump)使用します。
4.  フレームワークが提供するメッセージを表示するには、 [ **! wdfkd. wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)または[ **! wdfkd. wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)を使用します。

**UMDF ドライバーのライブデバッグ**

1.  WDF に現在動的にバインドされているドライバーに関する情報を表示するには、 [ **! wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)拡張機能を使用します。 ユーザーモードドライバーを検索します。 関連付けられているホストプロセスを入力します。
2.  「 **! Wdfkd. wdflogdump** 」と入力します。この *&lt;、&lt;フラグ&gt;に&gt;* ます。 *&lt;フラグ&gt;* は次のとおりです。

    -   0x1 –マージされたフレームワークとドライバーのログ
    -   0x2: ドライバーログ
    -   0x3 –フレームワークログ

    指定されたドライバーのドライバーログがない場合、拡張機能にはフレームワークのログのみが表示されます。

**UMDF ドライバークラッシュ後の Inflight トレースレコーダーログの表示**

1. [WinDbg] から [&gt;ファイル] を選択して **[クラッシュダンプを開く]** を選択し、デバッグするミニダンプファイルを指定します。
2. 「 [ **! Wdfkd. wdfkd」と入力すると、*ドライバー&gt; ホストの &lt;プロセス ID&gt;&lt;*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)&lt;オプション&gt;&lt;&gt;*オプション*は次のようになります。

   -   0x1 –マージされたフレームワークとドライバーのログ
   -   0x2: ドライバーログ
   -   0x3 –フレームワークログ

   ドライバーを指定しない場合、 [ **! wdfcrashdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)によってすべてのドライバーの情報が表示されます。 ホストプロセスを指定せず、1つしか存在しない場合、拡張機能は単一のホストプロセスを使用します。 ホストプロセスを指定せず、複数のホストプロセスがある場合は、アクティブなホストプロセスの一覧が表示されます。

   ミニダンプに格納されているログ情報が入力した名前と一致しない場合、ミニダンプにはドライバーのログが含まれていません。

ドライバーにトレースメッセージを追加する方法の詳細については、「[ドライバーへの WPP マクロの追加](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)」を参照してください。

## <a name="related-topics"></a>関連トピック


[UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md)

[RCDRKD 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)

[フレームワークのイベントロガーの使用](using-the-framework-s-event-logger.md)

[UMDF ドライバーでの WPP ソフトウェアトレースの使用](using-wpp-software-tracing-in-umdf-drivers.md)

 

 






