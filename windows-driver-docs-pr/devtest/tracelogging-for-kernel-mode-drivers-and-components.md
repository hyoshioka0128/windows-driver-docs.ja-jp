---
title: カーネル モード ドライバーとコンポーネント用の TraceLogging
description: このトピックでは、カーネル モード ドライバーとコンポーネント内から TraceLogging API を使用する方法について説明します。
ms.assetid: 6AF8DD2C-400F-4E9D-A6DF-40A847BCBD76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b98d079b1c206957e4d92db710f24c0d8dffad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369696"
---
# <a name="tracelogging-for-kernel-mode-drivers-and-components"></a>カーネル モード ドライバーとコンポーネント用の TraceLogging

このトピックでは、使用する方法を説明します、 [TraceLogging](https://docs.microsoft.com/windows/desktop/tracelogging/trace-logging-portal)からカーネル モード ドライバーとコンポーネント内の API。

前提条件:

- Windows 10
- Visual Studio 2013 (またはそれ以降)
- Windows 10 SDK
- Windows 10 用 Windows Driver Kit (WDK)

## <a name="include-the-tracelogging-header-files"></a>TraceLogging ヘッダー ファイルを含める

TraceLogging API を使用するには、TraceLoggingProvider.h TraceLogging ヘッダー ファイルをインクルードします。 その他の TraceLogging API ヘッダー ファイル、TraceLoggingActivity.h はのみ C++ で記述されたユーザー モード ドライバーで使用できます。

```command
#include <wdm.h>
#include <TraceLoggingProvider.h> 
```

> [!NOTE]
> Wdm.h ファイルは、カーネル モード ドライバーを開発してが TraceLoggingProvider.h 必要です。

## <a name="declare-your-driver-as-a-tracelogging-provider"></a>TraceLogging プロバイダーとしてのドライバーを宣言します。

1. 追加、 [ **TRACELOGGING\_DECLARE\_プロバイダー** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_declare_provider)マクロをプロバイダーのハンドル変数を宣言します。 マクロでは、構文があります。

    ```command
    TRACELOGGING_DECLARE_PROVIDER(hProviderVariableName)
    ```

    次の例 TraceLogging ステートメントがという名前の変数を宣言*g\_hProvider*します。

    ```command
    TRACELOGGING_DECLARE_PROVIDER(g_hProvider);
    ```

    使用して宣言する変数[ **TRACELOGGING\_DECLARE\_プロバイダー** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_declare_provider)を呼び出すときにプロバイダーを識別するハンドルをなります、 [ **TRACELOGGING\_定義\_プロバイダー** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)コードでマクロ。

    > [!NOTE]
    > TraceLogging プロバイダーを識別するハンドルをグローバルに利用できるように、ヘッダー ファイルでこのマクロを配置することがあります。

2. 追加、 [ **TRACELOGGING\_を定義する\_プロバイダー** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)マクロは、トレース プロバイダー ハンドルと、トレース プロバイダーの名前を指定します。 ハンドルは、手順 1. で宣言された変数です。 マクロの構文です。

    ```command
    TRACELOGGING_DEFINE_PROVIDER(hProviderVariableName, "ProviderName", providerId [,option])
    ```

    たとえば、次のステートメントは MyTraceLoggingProviderKM と呼ばれるプロバイダーを定義し、g のハンドルに割り当てられます\_hProvider します。 ProviderId パラメーターは、ETW プロバイダー GUID です。

    ```command
    TRACELOGGING_DEFINE_PROVIDER(g_hProvider, "MyTraceLoggingProviderKM",
        (0xb3864c38, 0x4273, 0x58c5, 0x54, 0x5b, 0x8b, 0x36, 0x08, 0x34, 0x34, 0x71));
    ```

    [ **TRACELOGGING\_定義\_プロバイダー** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogging_define_provider)マクロ プロバイダーのストレージを割り当てるし、グローバル メモリ ハンドルをプロバイダーには、対応する変数を定義します。 プロバイダー名文字列リテラル (変数ではなく) 必要があり、含めることはできません '\\0' 文字。 ハンドルと、ハンドルのコピーは、元のハンドルがスコープ内に限り有効です。

    使用して、ハンドルを作成するとき、 **TRACELOGGING\_定義\_プロバイダー**マクロ、プロバイダーが登録されていない状態でします。 この状態で、プロバイダーは登録されるまでにトレース書き込み呼び出しを無視します。

    > [!NOTE]
    > カーネル モードの場合、注意がプロバイダーのメタデータが明示的に TLG に格納されている\_メタデータ\_セグメント (.rdata) ハンドルを作成する変数 (たとえば、g\_hProvider) と (プロバイダーの名前"MyTraceLoggingProviderKM"など) セグメントを明示的に割り当てられていないと、現在の暗黙的なセグメントを使用します。

**TRACELOGGING\_定義\_プロバイダー**マクロが非ページ プールに配置するために渡される変数が必要です。 これは、既に場合、呼び出し元が経由でデータ セグメントを設定する必要があります\#プラグマ データ\_seg (uniqueVarName) のまたは const のセグメントを使用して\#const プラグマ\_seg (g の\_hMyProvider) 呼び出す前に**TRACELOGGING\_定義\_プロバイダー**マクロ。

## <a name="register-the-driver-with-tracelogging"></a>TraceLogging にドライバーを登録します。

**DriverEntry**関数 TraceLogging プロバイダーを登録する必要があります。
TraceLogging にプロバイダーを登録するには、TraceLoggingRegister マクロを追加**DriverEntry**:

```command
// Register the TraceLogging provider in the DriverEntry method.
TraceLoggingRegister(g_hProvider);
```

## <a name="unregister-the-provider-in-the-driver-unload-or-cleanup-routine"></a>ドライバーのアンロードまたはクリーンアップ ルーチンでプロバイダーの登録を解除します。

**DriverUnload**またはクリーンアップ関数を TraceLogging プロバイダーの登録を解除します。

```command
// Stop TraceLogging and unregister the provider
TraceLoggingUnregister(g_hProvider);
```

## <a name="log-events-in-your-code"></a>ログ イベントをコードで

TraceLogging は、イベントのログ記録のマクロを提供します。

基本的なマクロは[ **TraceLoggingWrite**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-traceloggingwrite)します。 このマクロでは、次の構文があります。

```command
TraceLoggingWrite(g_hProvider, "EventName", args...)
```

場所 g\_hProvider は定義したプロバイダーのハンドルで、"EventName"は文字列リテラル (変数ではなく)、特定のイベントを識別するために使用します。 ような**printf**または**による DbgPrint**、 **TraceLoggingWrite**マクロは、さまざまな追加のパラメーター (最大 99) をサポートしています。 パラメーター (引数) などで TraceLogging ラッパーのマクロをする必要があります[ **TraceLoggingLevel**](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-tracelogginglevel)、 [TraceLoggingInt32](https://docs.microsoft.com/windows/desktop/tracelogging/tracelogging-wrapper-macros)、または[TraceLoggingString](https://docs.microsoft.com/windows/desktop/tracelogging/tracelogging-wrapper-macros). TraceLogging ラッパーのマクロは、TraceLoggingProvider.h で定義されます。

> [!NOTE]
> C++ を使用する場合は、使用、 [ **TraceLoggingValue** ](https://docs.microsoft.com/windows/desktop/api/traceloggingprovider/nf-traceloggingprovider-traceloggingvalue)ラッパー マクロを型に自動的に調整します。 C では、ドライバーを作成する場合は、型固有のフィールド マクロを使用する必要があります (たとえば、 **TraceLoggingInt32**または**TraceLoggingUnicodeString**)。

プロバイダーのイベントをログに次の例 g\_hProvider します。 イベントは"MyDriverEntryEvent"と呼ばれる マクロをトレース ログ ドライバー オブジェクトおよびレジストリ パスにポインターを書き込む TraceLoggingPointer と TraceLoggingUnicodeString ラッパーを利用します。 TraceLoggingUnicodeString ラッパーは、オプションの名前です。 この例では、"RegPath"は、RegistryPath 値の名前です。 名前が指定されていない場合、値は、名前として使用されます。

```command
TraceLoggingWrite(
        g_hProvider,
        "MyDriverEntryEvent",
        TraceLoggingPointer(DriverObject),
        TraceLoggingUnicodeString(RegistryPath, "RegPath")); 
);
```

カーネル モード ドライバー (C) で、インストルメント化する場合は、TraceLoggingProvider.h へのリンクを使用することができます、 **TraceLoggingWrite**、 **TraceLoggingWriteActivity**、または**TraceLoggingActivityMarker**マクロ。 トレース ログの例については、次を参照してください。 [TraceLogging 例](tracelogging-examples.md)します。

TraceLoggingProvider.h と TraceLoggingActivity.h にリンクする場合は、ドライバーまたは C++ で記述されたコンポーネントをインストルメント化は。 イベント ログに記録できる C++ ヘッダーにリンクすると、 **TraceLoggingWriteStart**、 **TraceLoggingWriteStop**、および**TraceLoggingWriteTagged**マクロ。

キャプチャして TraceLogging データを表示する方法の例については、次を参照してください。[キャプチャとビュー TraceLogging データ](capture-and-view-tracelogging-data.md)します。
