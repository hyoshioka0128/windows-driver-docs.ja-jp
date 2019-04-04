---
title: 64 ビット プリンター ドライバーの記述
description: 64 ビット プリンター ドライバーの記述
ms.assetid: 41f1a521-980e-4ccd-a395-e1d1bf0114d1
keywords:
- プリンター ドライバー WDK、64 ビット
- 64 ビットの WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a1c36223634ad720723c11b20cecbde29f3a2fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581074"
---
# <a name="writing-64-bit-printer-drivers"></a>64 ビット プリンター ドライバーの記述


64 ビット ドライバーを作成またはの 32 ビットと 64 ビットの両方のシステムでコンパイルできるドライバーを記述する場合に 64 ビット移植のガイドラインに従って[ドライバーのプログラミング手法](https://msdn.microsoft.com/library/windows/hardware/ff554452)します。 このトピックでは、いくつかの制限事項と 64 ビット プリンター ドライバーの書き込みで発生する可能性がある問題について説明します。

装飾を使用して、64 ビット アーキテクチャを特定する方法の詳細については、次のトピックを参照してください。

-   [プリンターの INF ファイルで装飾](decorations-in-printer-inf-files.md)

-   [プリンター ドライバーの INF ファイルで装飾を使用する方法](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

### <a name="limitations-on-device-context-handles"></a>デバイス コンテキスト ハンドルに関する制限事項

プリンター ドライバー プラグイン Splwow64.exe サンク プロセスのコンテキストで実行されているが、GDI を呼び出さない場合は、32 ビット アプリケーションは、Microsoft Windows オペレーティング システムの 64 ビット版で実行されて、**フォーマット**関数。この呼び出しは失敗します。

### <a name="problems-with-writing-64-bit-drivers"></a>64 ビット ドライバーの記述に関する問題

既存の 32 ビット ドライバー コードには、ポインター型や DWORD または ULONG などの整数型の間の変換に関して注意します。 32 ビットのコンピューターでコードを作成した経験がある場合は、ポインター値が DWORD または ULONG 適合と仮定するできます使用する可能性があります。 64 ビット コードでは、この想定は危険です。 DWORD または ULONG 型へのポインターをキャストすると、64 ビットのポインターは切り捨てられます。

代わりに、DWORD へのポインターをキャスト\_PTR または ULONG\_PTR。 DWORD 型の符号なし整数\_PTR または ULONG\_PTR は 32 ビットまたは 64 ビット コンピューターのコードをコンパイルするかどうかに関係なく、全体のポインターを格納するのに十分な大きさでは常にします。

PDrvOptItems.UserData ポインター フィールドなど、 [ **OEMCUIPPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff557653)構造体は ULONG 型\_PTR。 次のコード例は、このフィールドに 64 ビット ポインターの値をコピーする場合のように指定しない動作を示しています。

```cpp
    PUSERDATA pData;
    OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG)pData;  // Wrong
```

上記のコード例のキャスト、 *pData*場合、ポインター値を切り捨てることができる ULONG 型へのポインター **sizeof**(*pData*) &gt; **sizeof**(ULONG)。 正しいアプローチは、ULONG へのポインターをキャストする\_PTR、次のコード例に示すようにします。

```cpp
    PUSERDATA pData;
    OEMCUIPPARAM->pDrvOptItems.UserData = (ULONG_PTR)pData;  // Correct
```

上記のコード例では、ポインター値の 64 ビットをすべて保持されます。

などの 64 ビットのインライン関数**PtrToUlong**と**UlongToPtr**ポインターと整数型間でこれらの種類の相対的なサイズを推測に頼ることがなく安全に変換します。 1 つの型が他方より短い場合は、長い型に変換するときに拡張する必要があります。 短い型は符号ビット、または 0 で入力することで拡張は、各 Win64 関数は、このような状況を処理できます。 次のコード例を検討してください。

```cpp
    ULONG ulHWPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // wrong
```

上記のコード例を次のコード例と置き換える必要があります。

```cpp
    ULONG_PTR ulHWPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysHWBuffer) + HW_BUFFER_SIZE;  // correct
```

2 番目のコード例が優先される場合でも

```cpp
ulSlotPhysAddr
```

64 ビット長ではなく 32 ビット長のみであるハードウェア レジスタの値を表すことができます。 すべての新しい Win64 ヘルパー関数ポインターと整数型間の変換については、[、新しいデータ型](https://msdn.microsoft.com/library/windows/hardware/ff564619)を参照してください。
 

 




