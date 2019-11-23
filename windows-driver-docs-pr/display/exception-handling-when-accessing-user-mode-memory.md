---
title: ユーザー モード メモリにアクセスする際の例外処理
description: ユーザー モード メモリにアクセスする際の例外処理
ms.assetid: 44ed69a0-da0e-4335-9128-a78a83ea80dd
keywords:
- ユーザーモードメモリ WDK Windows 2000 ディスプレイ
- ユーザーモードメモリ WDK Windows 2000 ディスプレイ、例外処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f94333dfa7a5264dd55cf3a9af2b59c5760472e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838946"
---
# <a name="exception-handling-when-accessing-user-mode-memory"></a>ユーザー モード メモリにアクセスする際の例外処理


## <span id="ddk_exception_handling_when_accessing_user_mode_memory_gg"></span><span id="DDK_EXCEPTION_HANDLING_WHEN_ACCESSING_USER_MODE_MEMORY_GG"></span>


ディスプレイまたはビデオミニポートドライバーでは、ユーザーモードで割り当てられたデータ構造にアクセスするコードの周囲に例外処理を使用する必要があります。 Microsoft Direct3D ランタイムは、このようなデータ構造の所有権を、ドライバーに渡す前に保護します。 ユーザーモードメモリの所有権をセキュリティで保護するために、ランタイムは[**Mmsecurevirtualmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)関数を呼び出します。 ランタイムは、ユーザーモードのメモリの所有権をセキュリティで保護するときに、他のスレッドがメモリへのアクセスの種類を変更できないようにします。 たとえば、ランタイムが読み取りと書き込みのアクセス権を持つユーザーモードスレッドによって割り当てられたデータ構造の所有権をセキュリティで保護する場合、他のスレッドは、データ構造のアクセスの種類を読み取り専用に制限することはできません。 また、ユーザーモードメモリの所有権をセキュリティで保護しても、メモリが有効なままであることは保証されません。

そのため、このようなメモリにアクセスするコードに例外処理が実装されていない場合、ドライバーが無効なユーザーモードのメモリにアクセスしようとすると、オペレーティングシステムがクラッシュします。 無効なカーネルメモリアクセスの場合、オペレーティングシステムで使用可能なオプションはクラッシュのみです。 ただし、無効なユーザーメモリアクセスの場合、ドライバーは、メモリを無効にしたアプリケーションを終了し、オペレーティングシステムとドライバーのデバイスを安定した状態のままにすることができます。

ドライバーは、ランタイムに依存して例外を処理するのではなく、例外処理を実装する必要があります。 ランタイムが例外を処理し、ドライバーが無効なユーザーモードメモリにアクセスした場合、スタックはランタイムの例外処理コードに戻り、ドライバーまたはデバイスは不明な状態のままになります。 例外が発生した場合に次の操作を実行できるように、ドライバーは例外処理を実装する必要があります。

-   デバイスの状態と状態を復元します。

-   取得したすべてのスピンロックを解除します。

次のシナリオでは、ランタイムは、メモリをドライバーに渡す前に、ユーザーモードで割り当てられたメモリの所有権を保護します。

-   ドライバーは、ユーザーモードのメモリへのポインターによって指定された頂点データを処理します。 ドライバーは、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の呼び出しでこのメモリポインターを受信します。 この*D3dDrawPrimitives2*の呼び出しでは、 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体の**DWFLAGS**メンバーの D3DHALDP2\_usermemvertices フラグが設定されています。

-   ドライバーは、\_D3DHAL の**lpdwRStates**メンバーが DRAWPRIMITIVES2DATA ポイントを指すレンダリング状態の配列を更新します。 ドライバーは、 *D3dDrawPrimitives2*関数の呼び出し中にこの配列を更新します。

-   ドライバーは、 [**D3dGetDriverState**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)関数の呼び出し中に、 [**DD\_GETDRIVERSTATEDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverstatedata)構造体の**lpdwStates**メンバーで状態を更新します。

-   ドライバーのビットブロックは、ユーザーメモリに割り当てられたシステムテクスチャに転送またはアクセスします。

ディスプレイドライバーは、 **try/except**機構を使用して例外処理を実装できます。 **Try/except**の詳細については、Microsoft のC++ Visual ドキュメントを参照してください。

次のコード例は、無効なメモリにアクセスしたことが原因でエラーが発生した場合に、ドライバーが**try/except**機構を使用して例外をスローする方法を示しています。

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

**注**  ユーザー モードの値にアクセスしてローカル変数にコピーする以外に、ドライバーは **\_\_try** ブロック内で内で他の操作を行わないでください。 他の操作では、独自の例外が発生する可能性があります。 オペレーティングシステムでは、これらの例外は異なる方法で処理されます。

 

 

 





