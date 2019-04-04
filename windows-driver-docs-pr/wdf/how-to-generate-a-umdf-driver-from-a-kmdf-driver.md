---
title: KMDF ドライバーを 2 の UMDF ドライバー (およびその逆) に変換する方法
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーをユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバー、およびその逆に変換する方法について説明します。
ms.assetid: 69B865CF-65D0-4211-951B-6574E27F10BD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69cbfe374c5bc881741a320f52e74cfea00ed2fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538393"
---
# <a name="how-to-convert-a-kmdf-driver-to-a-umdf-2-driver-and-vice-versa"></a>KMDF ドライバーを 2 の UMDF ドライバー (およびその逆) に変換する方法


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーをユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバー、およびその逆に変換する方法について説明します。

## <a name="driver-conversion-using-visual-studio"></a>Visual Studio を使用してドライバーの変換


1.  KMDF から UMDF への切り替え、ときに、Visual Studio を使用して UMDF の空のプロジェクトを作成、**ユーザー モード ドライバー (UMDF V2) 空**プロジェクト テンプレート。 UMDF から KMDF への切り替え、ときに、Visual Studio を使用して KMDF の空のプロジェクトを作成、**カーネル モード ドライバーでは、空 (KMDF)** プロジェクト テンプレート。

    Visual Studio では、指定のフレームワークを対象とした、INF ファイルと共に、適切な設定で、空のドライバーのプロジェクトを作成します。

2.  新しいプロジェクトに、以前のドライバからソース コードとヘッダー ファイルをコピーします。
3.  ヘッダー ファイルを更新します。 Umdf、Windows.h が含まれます。 Kmdf、Ntddk.h が含まれます。 Wdf.h が KMDF と UMDF の両方に共通するには、そのドライバーのどちらの種類が含まれます。

    必要に応じて、使用、 **\_カーネル\_モード**プリプロセッサ マクロを条件付きで適切なシステム ヘッダーを追加します。

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

4.  削除するか、条件付きでコンパイルするには、ソース コードを更新 (を使用して、 **\_カーネル\_モード**マクロ) 機能をターゲット ドライバー モデルではサポートされていません。 次に、例を示します。

    -   ドライバーは、WPP トレースを使用している場合は、更新、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)マクロ。 このマクロは、ユーザー モードとカーネル モードで別のパラメーターを受け取ります。
        ```cpp
        WPP_INIT_TRACING ( DriverObject, RegistryPath ); // KMDF
        WPP_INIT_TRACING ( “<MyDriverNameString>” ); // UMDF
        ```

    -   KMDF ドライバーなど WDM ルーチンの呼び出しを変換するかどうか[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)など、WDF の対応するメソッドを置き換える[ **WdfMemoryCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548706)します。 同様に、ユーザー モード関数を呼び出す UMDF ドライバーを変換する場合は、これらのカーネル モードのと同じルーチンを置き換えます。
    -   いくつかのメソッドは、UMDF でのみサポートされていますが、他のユーザー、KMDF でのみサポートされます。 Windows Driver Frameworks (WDF) のすべてのメソッドと、フレームワークの適用性の一覧は、[WDF のコールバックの概要とメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265591)を参照してください。

 

 





