---
title: TraceMessage が呼び出される前に、最後のエラーコードを保持することはできますか。
description: TraceMessage が呼び出される前に、最後のエラーコードを保持することはできますか。
ms.assetid: 57390fb1-5e01-4b98-960f-0201213d673c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8305e09a0707cad2bf7a97f2ec40f8141db502de
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769644"
---
# <a name="can-i-preserve-the-last-error-code-before-tracemessage-is-called"></a>TraceMessage が呼び出される前の最後のエラー コードを保持できますか?


既定では、 [TraceMessage](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessage)は、WPP トレースマクロを使用して呼び出され \_ ます。 Windows Vista より前のバージョンの Windows では、 **TraceMessage**によって[最後のエラーコード](https://docs.microsoft.com/windows/win32/debug/last-error-code)が上書きされました。

Windows Vista 以降では、カスタムの WPP トレースマクロを定義することによって、最後のエラーコードを保持することができ \_ ます。 トレース[メッセージヘッダー (tmh) ファイル](trace-message-header-file.md)を[トレースプロバイダー](trace-provider.md)のソースファイル (カーネルモードドライバーやユーザーモードアプリケーションなど) に含める前に、このマクロのバージョンを定義する必要があります。「」をご確認ください。

次の例は、 **TraceMessage**を呼び出す前に最後のエラーコードを保持する方法を示しています。

-   WPP トレースマクロから呼び出される**TraceMessage**のラッパーを作成し \_ ます。 次に、ラッパー関数から[Tracemessageva](https://docs.microsoft.com/windows/win32/api/evntrace/nf-evntrace-tracemessageva)を呼び出すことができます。

    次の例は、 **TraceMessage**にラッパーを書き込む方法を示しています。

    ```
    #define WPP_TRACE WppTraceMessageWrapper
    DWORD
    WppTraceMessageWrapper(
        __in TRACEHANDLE LoggerHandle,
        __in ULONG MessageFlags,
        __in LPCGUID MessageGuid,
        __in USHORT Message Number,
        ...)
    {
        DWORD TraceError = ERROR_SUCCESS;
        DWORD LastError = ERROR_SUCCESS;
        va_list Args = NULL;
     
        LastError = GetLastError();
     
        va_start(Args, Message Number);
        TraceError = TraceMessageVa(LoggerHandle, MessageFlags, MessageGuid, Message Number, Args);
        va_end(Args);
     
        SetLastError(LastError);
     return TraceError;
    }
    ```

-   \_次の例に示すように、WPP トレースマクロを変更します。
    ```
    #define WPP_TRACE(...)                              \
     do                                              \
        {                                               \
            DWORD LastError = GetLastError();           \
            TraceMessage(__VA_ARGS__);                  \
            SetLastError(LastError);                    \
        }                                               \
     while (FALSE, FALSE)
    ```

    **メモ**   このメソッドは、各 WPP SF 関数に対して同じコードが生成されるため、バイナリファイルのコードサイズを増やし \_ ます。

     

 

 





