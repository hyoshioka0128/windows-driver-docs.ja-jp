---
title: 私を保持できます直前のエラー コード TraceMessage が呼び出される前に
description: 私を保持できます直前のエラー コード TraceMessage が呼び出される前に
ms.assetid: 57390fb1-5e01-4b98-960f-0201213d673c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea0614ceee3bc10330bebb08786c36b041c47666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557974"
---
# <a name="can-i-preserve-the-last-error-code-before-tracemessage-is-called"></a>TraceMessage が呼び出される前に直前のエラー コードを保持はできますか。


既定では、 [TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)によって、WPP を使用して呼び出される\_TRACE マクロ。 Windows Vista より前のバージョンの Windows で、[直前のエラー コード](https://go.microsoft.com/fwlink/p/?linkid=179346)で上書きされた**TraceMessage**します。

以降では、Windows Vista は、保持できる最新のエラー コード カスタム WPP を定義することで\_TRACE マクロ。 インクルードする前に、このマクロのバージョンを定義する必要があります、[トレース メッセージのヘッダー (.tmh) ファイル](trace-message-header-file.md)のソース ファイルで、[トレース プロバイダー](trace-provider.md)カーネル モード ドライバーまたはユーザー モード アプリケーションなど、.

次の例を呼び出す前に最終エラー コードを保持する方法を示します**TraceMessage**:

-   ラッパーを行う**TraceMessage** WPP から呼び出される\_TRACE マクロ。 呼び出して[TraceMessageVa](https://go.microsoft.com/fwlink/p/?linkid=179352)、ラッパー関数から。

    次の例は、ラッパーを作成する方法を示しています**TraceMessage**:。

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

-   変更、WPP\_トレース マクロは、次の例に示すようにします。
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

    **注**  各 WPP に対して同じコードを生成するために、このメソッドが、バイナリ ファイルのコード サイズを大きく\_SF 関数。

     

 

 





