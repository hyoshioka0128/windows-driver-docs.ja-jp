---
title: Windows 2000 ドライバーの初期化
description: Windows 2000 ドライバーの初期化
ms.assetid: 82222357-1e5a-4aec-879a-68f19f3faa4f
keywords:
- Windows 2000、Windows 2000 の WDK 表示 DirectDraw ドライバーの初期化
- Windows 2000 ディスプレイ ドライバー モデル WDK、DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a20c1dfd1acbf0e4c24de8079477a340ee385c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391130"
---
# <a name="windows-2000-driver-initialization"></a>Windows 2000 ドライバーの初期化


## <span id="ddk_windows_2000_driver_initialization_gg"></span><span id="DDK_WINDOWS_2000_DRIVER_INITIALIZATION_GG"></span>


Windows 2000 以降、アプリケーションによって要求されたときにドライバーの情報を取得のみです。 つまり、DirectDraw オブジェクトのインスタンスを作成する Microsoft DirectDraw アプリケーションの要求に応答して、グラフィックス エンジンは DirectDraw ドライバーを初期化するためにドライバー関数を呼び出します。

Windows 2000 以降、ブート時に、各モードの変更後、このシーケンスは実行されます。 これは、副作用です。 Windows 98 でやドライバーが通常ある、GDI モードと DirectDraw モードの 2 つの操作--のモード。 DirectDraw が実行されている場合、GDI ビットマップをキャッシュ、DirectDraw を (その逆に GDI モードで) すべてのメモリを与える代わりにそのことはできません。 この動作には、ウィンドウ表示のアプリケーション (DirectX を使用する web ページ) などが原因となった低下します。 そのため、Windows 2000 以降で、メモリの使用方法の詳細については連携する GDI と DirectDraw が必要です。 Permedia3 サンプル ドライバーに付属している Windows ドライバー開発キット (DDK) ではこれを行う方法の例を示します。 (前に、DDK、Windows Driver Kit \[WDK\])。

ドライバーの初期化シーケンスは、次の関数を呼び出すことによって実現されます。

-   [**DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)ハードウェアの機能に関する情報を取得します。 GDI は、この関数を 2 回呼び出します。

    -   最初の呼び出しでは、メモリ ヒープの表示と、ドライバーがサポートする Fourcc の数のサイズを決定します。 GDI 渡します**NULL**両方の*pvmList*と*pdwFourCC*パラメーター。 ドライバーを初期化して返す*pdwNumHeaps*と*pdwNumFourCC*パラメーターのみです。
    -   GDI 表示メモリとの最初の呼び出しから返される値に基づいて FOURCC メモリの割り当て後に、2 番目の呼び出しが行われた*pdwNumHeaps*と*pdwNumFourCC*パラメーター。 2 番目の呼び出しでは、ドライバーを初期化して返す*pdwNumHeaps*、 *pvmList*、 *pdwNumFourCC*、および*pdwFourCC*パラメーター。

    GDI の割り当ておよびを 0 に初期化、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造体*pHalInfo*ポイント。 *DrvGetDirectDrawInfo* 、DD の適切なメンバー関数を入力する必要があります\_HALINFO 構造体にドライバー固有の情報。

    -   ドライバーの適切なメンバーを初期化する必要があります、 [ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)ディスプレイのメモリの一般的な形式を記述する構造体。 参照してください[表示メモリ](display-memory.md)します。
    -   ドライバーの適切なメンバーを初期化する必要があります、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248) DirectDraw をドライバーのコア機能を記述する構造体。
    -   ドライバーをサポートするドライバーの GUID を送信することによってクエリ実行される DirectX の機能のいずれかのかどうかは[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)コールバック、ドライバーを初期化する必要があります、 **GetDriverInfo**ドライバーの] をポイントするにはメンバー *DdGetDriverInfo*コールバックし、セット、DDHALINFO\_GETDRIVERINFOSET ビット**dwFlags**します。
    -   ドライバーを設定する必要があります**dwSize**サイズ (バイト単位) の[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造体。
-   [**DrvEnableDirectDraw** ](https://msdn.microsoft.com/library/windows/hardware/ff556208) DirectDraw ハードウェアを有効にして、ドライバーのコールバック サポートの一部を決定する、ランタイムで使用します。 GDI の割り当ておよびを 0 に初期化、 [ **DD\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff550485)、 [ **DD\_SURFACECALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551721)と[ **DD\_PALETTECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551681)パラメーター構造体。 ドライバーには、次を実装するこれらのコールバックの各を実行する必要があります。

    -   コールバックをポイントする適切な構造体の対応するメンバーを設定します。
    -   設定の対応する DDHAL\_*XXX*\_*XXX*ビット、 **dwFlags**適切な構造体のメンバー。

    ドライバーを実装できますその*DrvEnableDirectDraw*関数を記載するコールバック関数をサポートしていることを示す[DirectDraw コールバック サポートを使用して DrvEnableDirectDraw](directdraw-callback-support-using-drvenabledirectdraw.md)します。

    ドライバーの*DrvEnableDirectDraw*実装は、DirectDraw でのみ使用するための表示メモリなどのハードウェア リソースを割り当てることができますも。

-   [**DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)を他のコールバック関数と、ドライバーがサポートする機能を取得します。

    ない場合**NULL**、 **GetDriverInfo**でコールバックが返される、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)ドライバーのによる構造体[ **DrvGetDirectDrawInfo**](https://msdn.microsoft.com/library/windows/hardware/ff556229)します。 GDI の割り当て、初期化、 [ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)構造と呼び出し*DdGetDriverInfo* で説明されているGuidごと**DD\_GETDRIVERINFODATA**セクションを参照します。 すべての Guid がで定義されている*ddrawint.h*します。

    ドライバーを実装できるその*DdGetDriverInfo*関数で指定されたコールバック関数をサポートしていることを示す[DirectDraw、Direct3D のコールバック サポートを使用して DdGetDriverInfo](directdraw-and-direct3d-callback-support-using-ddgetdriverinfo.md)します。

サーフェスのメモリのロック (かどうか、サーフェス全体またはサーフェスの一部)、アプリケーションとハードウェアできません得ること表面のメモリへのアクセスと同時にします。 これにより、エラーを発生してから、アプリケーションの表面のメモリに書き込み中にします。 さらに、アプリケーションは、表面のメモリがロックされるまで、フリップをページことはできません。

 

 





