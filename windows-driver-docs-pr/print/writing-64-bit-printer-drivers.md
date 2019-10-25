---
title: 64 ビット プリンター ドライバーの記述
description: 64 ビット プリンター ドライバーの記述
ms.assetid: 41f1a521-980e-4ccd-a395-e1d1bf0114d1
keywords:
- プリンタードライバー WDK、64ビット
- 64-bit WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d80723ccdf10843329b7d470605bb1ca6d8eaf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832101"
---
# <a name="writing-64-bit-printer-drivers"></a>64 ビット プリンター ドライバーの記述


64ビットのドライバーを記述する場合、または32ビットと64ビットの両方のシステムで実行するようにコンパイルできるドライバーを作成する場合は、[ドライバーのプログラミング手法](https://docs.microsoft.com/windows-hardware/drivers/kernel/miscellaneous-driver-programming-techniques)における64ビット移植のガイドラインに従ってください。 このトピックでは、64ビットのプリンタードライバーを記述する際に発生する可能性がある制限事項と問題について説明します。

装飾を使用して64ビットアーキテクチャを識別する方法の詳細については、次のトピックを参照してください。

-   [プリンターの INF ファイルでの装飾](decorations-in-printer-inf-files.md)

-   [プリンタードライバーの INF ファイルでの装飾の使用方法](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

### <a name="limitations-on-device-context-handles"></a>デバイスコンテキストハンドルに関する制限事項

32ビットアプリケーションが64ビットバージョンの Microsoft Windows オペレーティングシステムで実行されている場合、Splwow64 のサンプロセスのコンテキストで実行されているプリンタードライバープラグインは、GDI **Createdc**関数を呼び出すことはできません。この呼び出しは失敗します。

### <a name="problems-with-writing-64-bit-drivers"></a>64ビットドライバーの記述に関する問題

既存の32ビットドライバーコードでは、ポインター型と DWORD や ULONG などの整数型の間の変換に注意してください。 32ビットコンピューター用のコードを記述する経験がある場合は、ポインター値が DWORD または ULONG に収まると想定して使用することがあります。 64ビットコードの場合、この想定は危険です。 ポインターを DWORD または ULONG 型にキャストした場合、64ビットポインターが切り捨てられる可能性があります。

代わりに、ポインターを\_PTR または ULONG\_PTR の型にキャストします。 \_PTR\_PTR または ULONG 型の符号なし整数は、コードが32ビットまたは64ビットのコンピューター用にコンパイルされているかどうかに関係なく、常にポインター全体を格納するのに十分な大きさです。

たとえば、 [**Oemcuipparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam)構造体内の pDrvOptItems ポインターフィールドの型は、ULONG\_PTR です。 次のコード例は、64ビットポインター値をこのフィールドにコピーした場合に実行されないことを示しています。

```cpp
    PUSERDATA pData;
    OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG)pData;  // Wrong
```

前のコード例では、 *pdata*ポインターを ulong 型にキャストします。 **sizeof**(*pData*) &gt; **sizeof**(ulong) の場合、ポインター値を切り捨てることができます。 正しい方法は、次のコード例に示すように、ポインターを ULONG\_PTR にキャストすることです。

```cpp
    PUSERDATA pData;
    OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG_PTR)pData;  // Correct
```

上記のコード例では、すべての64ビットのポインター値が保持されます。

**PtrToUlong**や**UlongToPtr**などのインライン64ビット関数は、これらの型の相対的なサイズに関する仮定に依存せずに、ポインター型と整数型を安全に変換します。 一方の型が他方より短い場合は、長い型に変換するときに拡張する必要があります。 符号ビットまたは0を使用して短い型が拡張された場合、各 Win64 関数はこれらの状況を処理できます。 次のコード例について考えてみます。

```cpp
    ULONG ulHWPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // wrong
```

前のコード例を次のコード例に置き換える必要があります。

```cpp
    ULONG_PTR ulHWPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // correct
```

2番目のコード例は、

```cpp
ulSlotPhysAddr
```

は、64ビットの長さではなく32ビットのハードウェアレジスタの値を表す場合があります。 ポインター型と整数型の間で変換を行うための新しいすべての Win64 ヘルパー関数の一覧については、[新しいデータ型](https://docs.microsoft.com/windows-hardware/drivers/kernel/the-new-data-types)を参照してください。
 

 




