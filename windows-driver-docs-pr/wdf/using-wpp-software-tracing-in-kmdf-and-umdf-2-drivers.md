---
title: KMDF および UMDF 2 で実行中のトレース レコーダー (IFR) を使用してドライバー
description: Windows 10 以降、Windows ソフトウェア トレース前処理を使用して情報をデバッグする追加のドライバーを取得できるように、WDF ドライバーを構築できます。
ms.assetid: CA2A7ED3-4372-4EE9-8B04-042A8C864BD5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8deb7a4491b22e674fb1329dc7b5b8c42e17b59b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556948"
---
# <a name="using-inflight-trace-recorder-ifr-in-kmdf-and-umdf-2-drivers"></a>KMDF および UMDF 2 で実行中のトレース レコーダー (IFR) を使用してドライバー


Windows 10 以降、Windows ソフトウェア トレース前処理を使用して情報をデバッグする追加のドライバーを取得できるように、KMDF ドライバーまたは UMDF ドライバーを構築できます。 この機能は、転送トレース レコーダー (), 違いますと呼ばれる、KMDF バージョン 1.15 および UMDF 2.15 バージョン以降があります。

実行中のトレース記録ツールの拡張機能は、 [WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)します。 WPP トレースとは異なり、実行中のトレース レコーダーはなくても、接続されているトレース コンシューマーが続行されます。 フレームワークが、循環バッファーにメッセージを書き込むし、ドライバーでは、独自のメッセージは追加もできます。 各ドライバーでは、独自のログを持つため、1 つのログのドライバーの共有に関連付けられた複数のデバイス。

ログは、システムのクラッシュの後に回復されるため、非ページング メモリに格納されます。 さらに、実行中のトレース記録ログは、ミニダンプ ファイルに含まれます。

**実行中のトレースの記録を有効にして、ドライバーからメッセージを送信する方法**

1.  Microsoft Visual studio で、次の手順を実行します。

    -   ドライバー プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、**[プロパティ]** をクリックします。 ドライバーのプロパティ ページで次のようにクリックします。**構成プロパティ**、し**Wpp トレース**します。 **全般**] メニューの [設定**WPP トレースの実行**に**はい**します。

    -   移動します**プロパティ -&gt;Wpp トレース -&gt;関数とマクロ オプション**選択**WPP レコーダーを有効にする**します。

    -   [同じ] メニューで、次のように設定します。**構成データのスキャン**Trace.h など、トレース情報を含むファイル。

2.  WPP マクロを呼び出して各ソース ファイルに追加、 **\#含める**を識別するディレクティブ、[トレース メッセージのヘッダー (TMH) ファイル](https://msdn.microsoft.com/library/windows/hardware/ff553926)します。 ファイル名の形式である必要があります&lt;*ドライバー ソース ファイル名*&gt;**.tmh**します。

    たとえば、ドライバーが 2 つのソース ファイルで構成される場合が呼び出されます*MyDriver1.c*と*MyDriver2.c*、し*MyDriver1.c*含める必要があります。

    **\#include "MyDriver1.tmh"**

    *MyDriver2.c*含める必要があります。

    **\#include "MyDriver2.tmh"**

    Visual Studio で、ドライバーをビルドすると、WPP プリプロセッサを生成します。*tmh*ファイル。

3.  定義、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)ヘッダー ファイルでマクロ。 このマクロは定義 GUID と[トレース フラグ](https://msdn.microsoft.com/library/windows/hardware/ff553904)ドライバーのトレース メッセージ。

    Osrusbfx2 ドライバーのサンプルを定義 1 つのコントロールの GUID と 7 つのトレース フラグ Trace.h ヘッダー ファイルで次の例に示すようにします。

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

    この例では:

    -   **OsrUsbFxTraceGuid** {d23a0c5a-d307-4f0e-ae8e-E2A355AD5DAB} GUID のわかりやすい名前を指定します。
    -   トレース フラグは、ドライバーのハンドルをさまざまな種類の I/O 要求として生成されるトレース メッセージを区別するために使用されます。

4.  ドライバー (KMDF および UMDF 2 の両方) を呼び出す必要があります[ **WPP\_INIT\_カーネル モード ドライバー用トレース**](https://msdn.microsoft.com/library/windows/hardware/ff556193)ドライバー オブジェクトと、レジストリ パスから通常[**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff540807):

    ```cpp
    WPP_INIT_TRACING( DriverObject, RegistryPath );
    ```

    KMDF と UMDF 2 の両方のドライバーの呼び出しのトレースを非アクティブ化する[ **WPP\_カーネル モード ドライバーのクリーンアップを**](https://msdn.microsoft.com/library/windows/hardware/ff556183)から[ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDriverUnload*](https://msdn.microsoft.com/library/windows/hardware/ff541694):

    ```cpp
    WPP_CLEANUP( WdfDriverWdmGetDriverObject( Driver ));
    ```

    [ **WPP\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff556183)マクロが PDRIVER 型のパラメーターを受け取る\_オブジェクト、その場合、ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)が失敗した呼び出しスキップできます[ **WdfDriverWdmGetDriverObject** ](https://msdn.microsoft.com/library/windows/hardware/ff547218)代わりに、 **WPP\_クリーンアップ**WDM へのポインタードライバーのオブジェクト。

    UMDF 2.15 バージョン以降、UMDF ドライバーは、トレースの初期化と後処理のこれらのマクロのカーネル モードの署名を使用します。 これは、KMDF および UMDF 呼び出しが似てことを意味します。

5.  使用して、 [ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)マクロ、または[カスタマイズされたバージョン](https://msdn.microsoft.com/library/windows/hardware/ff542492)トレース メッセージを作成するのには、ドライバー、マクロの。

    次の例は、Osrusbfx2 ドライバーの使用方法を示しています。 その**TraceEvents**関数コードの部分では、読み取り要求の処理に当て。

    ```cpp
    if (Length > TEST_BOARD_TRANSFER_BUFFER_SIZE) {
        TraceEvents(TRACE_LEVEL_ERROR,
                    DBG_READ,
                    "Transfer exceeds %d\n",
                    TEST_BOARD_TRANSFER_BUFFER_SIZE);
     
        status = STATUS_INVALID_PARAMETER;
    }
    ```

    呼び出し**TraceEvents**トレース コント ローラーを使用する場合にトレース メッセージを生成、**トレース\_レベル\_エラー**レベルと**DBG\_読み取る**トレース フラグ。 メッセージには、ドライバーの定義済み定数の値が含まれています。**テスト\_ボード\_転送\_バッファー\_サイズ**します。

6.  ドライバーのログを使用する循環バッファーのサイズを変更するには、変更、**ログ ページ**次のレジストリの場所にレジストリ値。

    <a href="" id="for-umdf-"></a>UMDF:  

    **ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス\\&lt;YourDriver&gt;\\パラメーター\\Wdf**

    <a href="" id="for-kmdf-"></a>KMDF:  

    **HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\&lt;YourDriver&gt;\\Parameters\\Wdf**

    型の値をこの**REG\_DWORD**ページで、割り当てられたログ バッファーのサイズが含まれています。 有効な値は 0x1 から 0x10 です。

**KMDF ドライバー**

1.  」と入力して RCDRKD コマンドを読み込む **.load rcdrkd.dll**デバッガーでします。
2.  使用して、 [ **! wdfkd.wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803)拡張機能には、Windows Driver Frameworks (WDF) を動的に現在バインドされているドライバーに関する情報を表示します。
3.  使用[ **! rcdrkd.rcdrlogdump** ](https://msdn.microsoft.com/library/windows/hardware/hh920382)と[ **! rcdrkd.rcdrcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/hh920380)するドライバーを提供するメッセージを表示します。
4.  使用[ **! wdfkd.wdflogdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565805)または[ **! wdfkd.wdfcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565682)にフレームワークを提供するメッセージを参照してください。

**ライブ UMDF ドライバーのデバッグ**

1.  使用して、 [ **! wdfkd.wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803) WDF に動的に現在バインドされているドライバーに関する情報を表示拡張機能。 ユーザー モード ドライバーを検索します。 関連付けられているホスト プロセスを入力します。
2.  型 **! wdfkd.wdflogdump**  *&lt;YourDriverName.dll&gt; &lt;フラグ&gt;* ここで、 *&lt;フラグ&gt;* は。

    -   0x1-framework とドライバーのログをマージ
    -   0x2-ドライバーのログ
    -   0x3-フレームワークのログ

    指定されたドライバーのドライバーのログがない場合は、拡張機能には、フレームワーク ログのみが表示されます。

**UMDF ドライバー クラッシュ後に実行中のトレース記録ログの表示**

1. WinDbg から次のように選択します。**ファイル -&gt;オープン クラッシュ ダンプ**、デバッグするには、ミニダンプ ファイルを指定します。
2. 型[ **! wdfkd.wdfcrashdump  *&lt;YourDriverName.dll&gt; &lt;ドライバー ホストのプロセス ID&gt; &lt;オプション&gt;***](https://msdn.microsoft.com/library/windows/hardware/ff565682)ここで、 *&lt;オプション&gt;* は。

   -   0x1-framework とドライバーのログをマージ
   -   0x2-ドライバーのログ
   -   0x3-フレームワークのログ

   ドライバーを指定しない場合は[ **! wdfcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565682)すべてのドライバーの情報が表示されます。 ホスト プロセスを指定しない 1 つしかない場合は、拡張機能は、1 つのホスト プロセスを使用します。 ホスト プロセスを指定しない 1 つ以上を使用する必要がある場合は、拡張機能には、アクティブなホスト プロセスが一覧表示します。

   ミニダンプに格納されたログ情報が入力した名前が一致しない場合は、ミニダンプには、ドライバーのログが含まれていません。

トレース メッセージをドライバーを追加する方法の詳細については、次を参照してください。[ドライバーに WPP マクロを追加する](https://msdn.microsoft.com/library/windows/hardware/ff541243)します。

## <a name="related-topics"></a>関連トピック


[UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md)

[RCDRKD 拡張機能](https://msdn.microsoft.com/library/windows/hardware/hh920376)

[フレームワークのイベントのロガーを使用します。](using-the-framework-s-event-logger.md)

[UMDF ドライバーでのトレース WPP ソフトウェアを使用します。](using-wpp-software-tracing-in-umdf-drivers.md)

 

 






