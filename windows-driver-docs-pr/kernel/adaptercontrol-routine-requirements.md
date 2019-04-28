---
title: AdapterControl ルーチンの要件
description: AdapterControl ルーチンの要件
ms.assetid: 09ce4ad8-eb1b-4fd0-9a22-4249d09584b3
keywords:
- AdapterControl ルーチン、要件
- 書き込みの AdapterControl ルーチン
- アダプター オブジェクトの WDK カーネル、AdapterControl ルーチンを記述
- AdapterControl ルーチンを記述、DMA 転送 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 317f38427cf05454e11c3a2553399d4d2cfc5ad6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365857"
---
# <a name="adaptercontrol-routine-requirements"></a>AdapterControl ルーチンの要件





少なくとも、 [ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチンは、次を実行する必要があります。

1.  入力を保存*MapRegisterBase*値と、ドライバーは IRP が現在の 1 つまたは複数の DMA 転送操作を実行する必要があるその他のコンテキスト情報。 ドライバーを渡す必要があります、 *MapRegisterBase*値を[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)各 DMA 転送操作が完了するとします。

2.  適切な返す[ **IO\_割り当て\_アクション**](https://msdn.microsoft.com/library/windows/hardware/ff550534)値。

    -   **KeepObject**のため、ドライバーはシステム DMA を使用して、デバイスが下位のデバイスの場合。

    -   **DeallocateObjectKeepRegisters**のため、ドライバーがパケットに基づく、バス マスター DMA を使用して、デバイスがバス マスターがかどうか。

ドライバーの設計によってその*AdapterControl*ルーチンも以下を実行前に、コントロールを返します。

1.  デバイス上で転送の開始位置を決定します。

2.  転送の開始位置のため、デバイスの制限を指定可能であれば、転送のサイズを計算します。

    呼び出すルーチンの責任は一般に、 [ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)によりプラットフォーム固有部分の転送転送要求を分割する必要があるかどうかを判断するには上の制限事項、 *NumberOfMapRegisters*ごとに利用可能な DMA、前のセクションで説明したように、操作を転送およびに記載された[転送要求の分割](splitting-dma-transfer-requests.md)します。

3.  ドライバーで維持される各転送デバイス (またはコント ローラー) で要求の拡張機能に関する状態を設定します。

    たとえば、 *AdapterControl*ルーチンを呼び出すことができます[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)のエントリ ポイントで、 [ *CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ドライバーの DMA 転送操作がタイムアウトするルーチン。

4.  呼び出す[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)に渡される MDL ポインター **Irp -&gt;MdlAddress**渡すに適した、転送の開始インデックスを取得するには[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)します。

5.  呼び出す**MapTransfer**システム DMA コント ローラーを設定するか、バス マスター デバイスの物理-論理アドレス マッピングを取得します。

6.  転送操作では、ドライバーのデバイスを使用して、プログラム、 [ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチンの呼び出しによって呼び出される[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302). 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

譲渡要求が、ドライバーを現在、ドライバーの IRP を満たすために部分的な転送操作のシーケンスを実行する必要があるかどうか[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンは通常、後続の転送操作のデバイスを再プログラミング責任を負います。 *AdapterControl* IRP の各着信転送のルーチンを 1 回だけ呼び出されます。

通常、IRP の現在の転送が完了するとドライバーのルーチン、 *DpcForIsr*または*CustomDpc*ルーチンも呼び出すことによって、DMA コント ローラーのシステムまたはバス マスター アダプターを解放する必要が[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)または[ **FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)、それぞれします。 このドライバーのルーチンが呼び出しを行う適切なできるだけ早く DMA の下位のデバイスのドライバーがシステム DMA コント ローラーに割り当てることができるまたはバス マスターのドライバーが次の転送の処理を開始することができるように、その最後の部分転送操作が行われるときIRP 速やかにします。

 

 




