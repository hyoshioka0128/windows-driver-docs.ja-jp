---
title: KMDF ドライバーを UMDF 2 ドライバーに変換する方法 (およびその逆)
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーをユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーに変換する方法について説明します。
ms.assetid: 69B865CF-65D0-4211-951B-6574E27F10BD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 997c47d97ad3489af5ceff825300a6debcc67289
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845217"
---
# <a name="how-to-convert-a-kmdf-driver-to-a-umdf-2-driver-and-vice-versa"></a>KMDF ドライバーを UMDF 2 ドライバーに変換する方法 (およびその逆)


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーをユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーに変換する方法について説明します。

## <a name="driver-conversion-using-visual-studio"></a>Visual Studio を使用したドライバーの変換


1.  KMDF から UMDF に切り替える場合は、Visual Studio で、**ユーザーモードドライバー、空 (Umdf V2)** プロジェクトテンプレートを使用して、空の UMDF プロジェクトを作成します。 UMDF から KMDF に切り替える場合は、Visual Studio で、**カーネルモードドライバー、空 (kmdf)** プロジェクトテンプレートを使用して、空の kmdf プロジェクトを作成します。

    Visual Studio は、指定されたフレームワークを対象とする INF ファイルと共に、適切な設定で空のドライバープロジェクトを作成します。

2.  前のドライバーのソースコードとヘッダーファイルを新しいプロジェクトにコピーします。
3.  ヘッダーファイルを更新します。 UMDF の場合は、Windows .h をインクルードします。 KMDF の場合は、Ntddk をインクルードします。 Wdf は KMDF と UMDF の両方に共通するため、両方の種類のドライバーに含めます。

    必要に応じて、 **\_KERNEL\_MODE**プリプロセッサマクロを使用して、適切にシステムヘッダーを条件付きで追加します。

    ```cpp
    #ifndef _KERNEL_MODE
    // This is a user-mode driver
    #include <windows.h>

    #else
    // This is a kernel-mode driver
    #include <ntddk.h>
    #define NTSTRSAFE_LIB
    #include <ntstrsafe.h>
    #endif

    // This is a common WDF header (for both KMDF and UMDF)
    #include <wdf.h> 
    ```

4.  ソースコードを更新して、ターゲットドライバーモデルでサポートされていないすべての機能を削除するか、条件付きでコンパイルします ( **\_KERNEL\_MODE**マクロを使用します)。 次に、例を示します。

    -   ドライバーで WPP トレースを使用する場合は、 [wpp\_INIT\_tracing](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロを更新します。 このマクロは、ユーザーモードとカーネルモードで異なるパラメーターを受け取ります。
        ```cpp
        WPP_INIT_TRACING ( DriverObject, RegistryPath ); // KMDF
        WPP_INIT_TRACING ( “<MyDriverNameString>” ); // UMDF
        ```

    -   [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)などの WDM ルーチンを呼び出す kmdf ドライバーを変換する場合は、 [**Wdfmemorycreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)など、対応する WDF メソッドで置き換えます。 同様に、ユーザーモード関数を呼び出す UMDF ドライバーを変換する場合は、これらを同等のカーネルモードルーチンに置き換えます。
    -   一部のメソッドは KMDF でのみサポートされていますが、他のメソッドは、UMDF でのみサポートされています。 すべての Windows Driver Framework (WDF) メソッドとそのフレームワークの適用性の一覧については、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。

 

 





