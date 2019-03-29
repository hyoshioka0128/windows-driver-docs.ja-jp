---
title: 64 ビット オーディオ ドライバーの作成
description: 64 ビット オーディオ ドライバーの作成
ms.assetid: 0b4cbb98-506e-443f-bac2-59dbdbcb1798
keywords:
- オーディオ ドライバー WDK、64 ビット
- 64 ビットの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25e467697d1e495fef1fb2553c5d3af67dde6daf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580334"
---
# <a name="writing-64-bit-audio-drivers"></a>64 ビット オーディオ ドライバーの作成


## <span id="writing_64_bit_audio_drivers"></span><span id="WRITING_64_BIT_AUDIO_DRIVERS"></span>


64 ビット ドライバーを作成または、両方の 32 ビットおよび 64 ビット システムで実行するコンパイルできるドライバーを記述する場合の移植のガイドラインに従って[ドライバーのプログラミング手法](https://msdn.microsoft.com/library/windows/hardware/ff554452)します。 64 ビットのオーディオ ドライバーの書き込みで発生する可能性が落とし穴を以下に示します。

第一に、既存の 32 ビット ドライバー コード内で検索する潜在的な問題は、ポインター型との DWORD またはこれ ULONG などの整数型間の変換です。 32 ビットのコンピューターでコードの記述経験のあるプログラマは、ポインター値が DWORD または ULONG に適合すると仮定した場合に使用可能性があります。 64 ビット コードでは、この想定は危険です。 DWORD または ULONG 型へのポインターをキャストすると、64 ビットのポインターが切り捨てられる可能性があります。 DWORD へのポインターをキャストするほうが効果的\_PTR または ULONG\_PTR。 DWORD 型の符号なし整数\_PTR または ULONG\_PTR は 32 ビットまたは 64 ビット コンピューターのコードをコンパイルするかどうかに関係なく、全体のポインターを格納するのに十分な大きさでは常にします。

たとえば、 [ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)ポインター フィールド**IoStatus**.**情報**ULONG 型は\_PTR。 次のコードでは、このフィールドに 64 ビット ポインターの値をコピーするときにしないは示しています。

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG)pDeviceRelations;  // wrong
```

このコード サンプルが誤ってキャスト、`pDeviceRelations`場合、ポインター値を切り捨てることができる ULONG 型へのポインター`sizeof(pDeviceRelations) > sizeof(ULONG)`します。 正しいアプローチは、ULONG へのポインターをキャストする\_PTR では、次に示すようにします。

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG_PTR)pDeviceRelations;  // correct
```

これには、すべての 64 ビットのポインター値が保持されます。

リソースの一覧は、リソースの物理アドレスを物理型の構造体に格納\_アドレス (を参照してください[IResourceList](https://msdn.microsoft.com/library/windows/hardware/ff536976))。 64 ビット アドレスの切り捨てを回避するには、構造体のアクセスする必要があります**QuadPart**メンバーではなく、**下位**メンバー構造体、または、アドレスからの読み取りにアドレスをコピーするときに、構造体。 たとえば、 **FindTranslatedPort**マクロへのポインターを返します、 [ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)I/O ポートのベース アドレスを格納する構造体。 **U**.**ポート**.**開始**この構造体のメンバーは物理\_ベース アドレスへのポインターのアドレス。 次のコードを表示しません。

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.LowPart;  // wrong
```

ここでも、このポインターを切り捨てることができます。 代わりに、アクセスする必要があります、 **QuadPart**では、次に示すように、このメンバーの。

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.QuadPart;  // correct
```

これは、全体の 64 ビット ポインターをコピーします。

などの関数をインライン Win64 **PtrToUlong**と**UlongToPtr**ポインターと整数型間でこれらの種類の相対的なサイズを推測に頼ることがなく安全に変換します。 1 つの型が他方より短い場合は、長い型に変換するときに拡張する必要があります。 によって短い型を拡張するかどうかまたは 0 で、符号ビットでいっぱいになるは Win64 関数ごとに適切に定義します。 つまり、任意のコード スニペットなど

```cpp
    ULONG ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // wrong
```

を置き換える必要があります。

```cpp
    ULONG_PTR ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // correct
```

これは、方法が望ましい場合でも`ulSlotPhysAddr`32 のみであるハードウェア レジスタの値を表すことができます 64 ビット長ではなく。 すべての新しい Win64 ヘルパー関数ポインターと整数型間の変換については、次を参照してください。 [、新しいデータ型](https://msdn.microsoft.com/library/windows/hardware/ff564619)します。

 

 




