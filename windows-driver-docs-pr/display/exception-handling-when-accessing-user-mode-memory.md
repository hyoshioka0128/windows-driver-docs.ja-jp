---
title: ユーザー モード メモリにアクセスする際の例外処理
description: ユーザー モード メモリにアクセスする際の例外処理
ms.assetid: 44ed69a0-da0e-4335-9128-a78a83ea80dd
keywords:
- ユーザー モード メモリ WDK Windows 2000 の表示
- ユーザー モード メモリ WDK Windows 2000 の表示、例外処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a55b57c829e91642c3abcdb3b93ff5369d2a935
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391250"
---
# <a name="exception-handling-when-accessing-user-mode-memory"></a>ユーザー モード メモリにアクセスする際の例外処理


## <span id="ddk_exception_handling_when_accessing_user_mode_memory_gg"></span><span id="DDK_EXCEPTION_HANDLING_WHEN_ACCESSING_USER_MODE_MEMORY_GG"></span>


表示またはビデオのミニポート ドライバーは、例外がユーザー モードで割り当てられているデータ構造にアクセスするコードの周り処理を使用する必要があります。 マイクロソフトの Direct3D ランタイムは、ドライバーに渡す前にこのようなデータ構造の所有権を保護します。 ユーザー モードのメモリの所有権をセキュリティで保護された、共通言語ランタイムは、 [ **MmSecureVirtualMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff556374)関数。 ランタイムは、ユーザー モードのメモリの所有権をセキュリティ保護、メモリへのアクセスの種類を変更することから、他のスレッドができないようにします。 たとえば、この場合は、ランタイムは、読み取り/書き込みアクセスをユーザー モード スレッドが割り当てられているデータ構造の所有権をセキュリティ保護、他のスレッドは読み取り専用にデータ構造体のアクセスの種類を制限できません。 また、ユーザー モードのメモリの所有権をセキュリティ保護は保証されません、メモリが有効に。

そのため、このようなメモリにアクセスするコードの周りを例外処理を実装しない限り、オペレーティング システムによって、無効なユーザー モード メモリにアクセスしようとすると、ドライバーがクラッシュします。 無効なカーネル メモリへのアクセス、オペレーティング システムにのみ利用可能なオプションではクラッシュ、です。 ただし、無効なユーザー メモリへのアクセスのドライバーできますアプリケーションを終了、メモリを無効と安定した状態で、オペレーティング システムとドライバーのデバイスのままにします。

ドライバーをランタイム例外を処理するには依存せずに例外処理を実装する必要があります。 例外とドライバーのアクセスの無効なユーザー モード メモリに、ランタイムが処理される場合、スタックは、ランタイムは、不明な状態のまま、ドライバーまたはデバイスでの例外処理コードに戻ります。 ドライバーは、例外処理、例外が発生した場合、次の操作を実行できますを実装する必要があります。

-   状態とそのデバイスの状態を復元します。

-   取得したすべてのスピン ロックを解放します。

次のシナリオでは、ランタイムは、メモリをドライバーに渡す前に、ユーザー モードで割り当てられたメモリの所有権を保護します。

-   ドライバーは、ユーザー モード メモリへのポインターで指定された頂点データを処理します。 ドライバーでは、このメモリ ポインターを受け取るへの呼び出しでその[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)関数。 この*D3dDrawPrimitives2*を呼び出すと、D3DHALDP2\_USERMEMVERTICES フラグ、 **dwFlags**のメンバー、 [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)構造体を設定します。

-   ドライバーでは、レンダリング状態の配列を更新する、 **lpdwRStates** D3DHAL のメンバー\_DRAWPRIMITIVES2DATA ポイント。 ドライバーでは、この配列を更新の呼び出し中にその*D3dDrawPrimitives2*関数。

-   ドライバー更新の状態で、 **lpdwStates**のメンバー、 [ **DD\_GETDRIVERSTATEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551551)構造体への呼び出し中にその[ **D3dGetDriverState** ](https://msdn.microsoft.com/library/windows/hardware/ff544708)関数。

-   ドライバーのビット ブロック転送またはメモリをユーザーに割り当てられたシステム テクスチャにアクセスします。

ディスプレイ ドライバーを使用して、**試用/を除く**例外処理を実装するためのメカニズムです。 詳細については**試用/を除く**、Microsoft Visual C のドキュメントを参照してください。

次のコード例は、ドライバーの使用方法を示しています、**試用/を除く**無効なメモリにアクセスするために、エラーが発生した場合に例外をスローするためのメカニズムです。

```cpp
__try
{
    // Access user-mode memory.
}
__except(EXCEPTION_EXECUTE_HANDLER)
{
    // Recover and leave driver and hardware in a stable state.
}
```

**注**  とは別にアクセスして、ローカル変数にユーザー モードの値をコピー、ドライバーを行わないで内で他の操作、  **\_\_お試しください**ブロックします。 その他の操作には、独自の例外が発生する可能性があります。 これらの例外の処理は、オペレーティング システムによって異なります。

 

 

 





