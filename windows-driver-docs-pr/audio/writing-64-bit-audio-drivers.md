---
title: 64 ビット オーディオ ドライバーの作成
description: 64 ビット オーディオ ドライバーの作成
ms.assetid: 0b4cbb98-506e-443f-bac2-59dbdbcb1798
keywords:
- オーディオドライバー WDK、64ビット
- 64-bit WDK audio
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ffeb2cc777ab932327f60d7f5f8a317c05b82e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829926"
---
# <a name="writing-64-bit-audio-drivers"></a>64 ビット オーディオ ドライバーの作成


## <span id="writing_64_bit_audio_drivers"></span><span id="WRITING_64_BIT_AUDIO_DRIVERS"></span>


64ビットドライバーを記述する場合、または32と64ビットシステムの両方で実行するようにコンパイルできるドライバーを作成する場合は、[ドライバーのプログラミング手法](https://docs.microsoft.com/windows-hardware/drivers/kernel/miscellaneous-driver-programming-techniques)に関するガイドラインに従ってください。 64ビットオーディオドライバーを記述する際に発生する可能性がある落とし穴の一部を次に示します。

まず、既存の32ビットドライバーコードで検索する可能性のある問題は、ポインター型と DWORD や ULONG などの整数型の間の変換です。 32ビットコンピューター用のコードを記述しているプログラマは、ポインター値が DWORD または ULONG に収まると想定するために使用されることがあります。 64ビットコードの場合、この想定は危険です。 ポインターを DWORD または ULONG 型にキャストすると、64ビットポインターが切り捨てられる可能性があります。 より優れたアプローチは、ポインターを ptr\_PTR または ULONG\_PTR にキャストすることです。 \_PTR\_PTR または ULONG 型の符号なし整数は、コードが32または64ビットコンピューター用にコンパイルされているかどうかに関係なく、常にポインター全体を格納するのに十分な大きさです。

たとえば、 [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)ポインターフィールド**iostatus**です。**情報**の種類は、\_PTR です。 次のコードは、64ビットポインター値をこのフィールドにコピーするときに行わないことを示しています。

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG)pDeviceRelations;  // wrong
```

このコードサンプルでは、`pDeviceRelations` ポインターを誤って型 ULONG にキャストしています。この場合、`sizeof(pDeviceRelations) > sizeof(ULONG)`するとポインター値が切り捨てられる可能性があります。 正しい方法は、次に示すように、ポインターを ULONG\_PTR にキャストすることです。

```cpp
    PDEVICE_RELATIONS pDeviceRelations;
    Irp->IoStatus.Information = (ULONG_PTR)pDeviceRelations;  // correct
```

これにより、すべての64ビットのポインター値が保持されます。

リソースの一覧には、リソースの物理アドレスが物理\_アドレス型の構造に格納されます (「 [Iresourcelist](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iresourcelist)」を参照してください)。 64ビットアドレスが切り捨てられないようにするには、構造体にアドレスをコピーするとき、または構造体からアドレスを読み取るときに、 **Lowpart**メンバーではなく、構造体の**QuadPart**メンバーにアクセスする必要があります。 たとえば、 **FindTranslatedPort**マクロは、i/o ポートのベースアドレスを格納している[ **\_リソース\_記述子構造体\_CM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)へのポインターを返します。 **U**.**ポート**。この構造体の**開始**メンバーは、ベースアドレスへの物理\_アドレスポインターです。 次のコードは、実行しないことを示しています。

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.LowPart;  // wrong
```

ここでも、ポインターを切り捨てることができます。 代わりに、次に示すように、このメンバーの**QuadPart**にアクセスする必要があります。

```cpp
    PUSHORT pBase = (PUSHORT)FindTranslatedPort(0)->u.Port.Start.QuadPart;  // correct
```

これにより、64ビットポインター全体がコピーされます。

**PtrToUlong**や**UlongToPtr**などのインラインの Win64 関数は、これらの型の相対サイズに関する仮定に依存せずに、ポインター型と整数型を安全に変換します。 一方の型が他方より短い場合は、長い型に変換するときに拡張する必要があります。 符号ビットを埋め込むか、または0を指定して、短い型を拡張するかどうかは、各 Win64 関数に対して適切に定義されます。 これは、次のようなコードスニペットがあることを意味します。

```cpp
    ULONG ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = ULONG(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // wrong
```

に置き換える

```cpp
    ULONG_PTR ulSlotPhysAddr[NUM_PHYS_ADDRS];
    ulSlotPhysAddr[0] = PtrToUlong(pulPhysDmaBuffer) + DMA_BUFFER_SIZE;  // correct
```

これは、`ulSlotPhysAddr` が64ビット長ではなく32であるハードウェアレジスタの値を表している可能性がある場合でも推奨されます。 ポインター型と整数型の間で変換を行うための新しいすべての Win64 ヘルパー関数の一覧については、[新しいデータ型](https://docs.microsoft.com/windows-hardware/drivers/kernel/the-new-data-types)を参照してください。

 

 




