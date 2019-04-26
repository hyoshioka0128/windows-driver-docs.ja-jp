---
title: DMA 操作インターフェイスのバージョン 3
description: バージョン 3 の DMA 操作インターフェイスでは、Windows 8 以降で使用できます。
ms.assetid: EFB59930-7D58-4E6E-8242-66A326E239E5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7633e221a34c4ac09c77ce11797512a0bdf1d901
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355250"
---
# <a name="version-3-of-the-dma-operations-interface"></a>DMA 操作インターフェイスのバージョン 3


バージョン 3 の DMA 操作インターフェイスでは、Windows 8 以降で使用できます。 **DMA\_操作**構造にこのインターフェイスには、以前のバージョンのこのインターフェイスで定義されていない新しいルーチンの数値が含まれています。 バージョン 3 のルーチンの一覧は、次を参照してください。 [ **DMA\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544071)します。

このインターフェイスはチップ (SoC) のシステムの統合で DMA コント ローラーのシステムの高度な機能を使用するカーネル モード ドライバーを有効にする多くの機能でバージョン 3 の DMA 操作インターフェイスは、すべての Windows ハードウェア プラットフォームで使用できますが、回線。 通常、これらの機能には、スキャッター/ギャザー DMA 転送実行する機能が含まれます。 これに対し、以前のバージョンの DMA 操作のインターフェイスは、バス マスターのデバイスにスキャッター/ギャザー DMA の転送を制限します。 バージョン 3 のインターフェイスは、スキャッター/ギャザー リストの管理を簡略化し、複雑な DMA 転送中にドライバーの介入の必要性が軽減します。

バージョン 3 の DMA 操作インターフェイスを使用して、DMA の転送を実行する、ドライバーは通常、次のルーチンを呼び出します。

<a href="" id="iogetdmaadapter"></a>[**IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)  
DMA のアダプター オブジェクトを割り当てるしへのポインターを返します、 [ **DMA\_アダプター** ](https://msdn.microsoft.com/library/windows/hardware/ff544062) DMA 操作のインターフェイスを含む構造体。

<a href="" id="getdmatransferinfo"></a>[**GetDmaTransferInfo**](https://msdn.microsoft.com/library/windows/hardware/hh451125)  
呼び出し元によって定義された DMA の転送を実行するために必要なリソースの説明を提供します。

<a href="" id="allocateadapterchannelex"></a>[**AllocateAdapterChannelEx**](https://msdn.microsoft.com/library/windows/hardware/hh406340)  
DMA の転送に必要なリソースを割り当てるし、DMA アダプター オブジェクトにこれらのリソースを割り当てます。

<a href="" id="maptransferex"></a>[**MapTransferEx**](https://msdn.microsoft.com/library/windows/hardware/hh406521)  
DMA の転送にマップ レジスタとスキャッター/ギャザー バッファーを初期化し、転送を開始します。

<a href="" id="flushadapterbuffersex"></a>[**FlushAdapterBuffersEx**](https://msdn.microsoft.com/library/windows/hardware/hh451102)  
DMA 転送の最後に必要な可能性があるキャッシュの操作を実行します。

<a href="" id="freeadapterchannel"></a>[**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)  
DMA チャネルとマップのレジスタを解放します。

<a href="" id="putdmaadapter"></a>[**PutDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff559965)  
アダプター オブジェクトを解放します。

これらのルーチンは、専用の DMA コント ローラーを使用するバス マスター デバイスとシステム DMA コント ローラーを共有する下位のデバイスの両方に使用されます。 一般的な DMA 転送中に、ドライバーは、呼び出しの詳細な手順については、次を参照してください。 [DMA のルーチンのバージョン 3 の基本的な呼び出しパターン](basic-calling-pattern-for-version-3-dma-routines.md)します。

**注**   DMA 操作のインターフェイスのバージョン 3 で呼び出し、 [ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)ルーチンは前に、または後 DMA 転送は必要ありません。 理由は、次のルーチンの対象にハードウェア キャッシュの一貫性を強制しないプラットフォームでのデータ キャッシュをフラッシュする必要があることを示します。

-   **MapTransferEx**により、プロセッサのデータ キャッシュは、書き込み (メモリ デバイス) を転送する前にフラッシュされます。
-   **FlushAdapterBuffersEx**により、読み取り (デバイスのメモリ) の転送後のキャッシュが無効になります。

X86 または x64 プロセッサでは、上、 **KeFlushIoBuffers**呼び出しは、操作を実行しないと、この呼び出し中に、不要なに支障をきたさないハードウェア プラットフォームの操作。 呼び出し、ARM プロセッサ上**KeFlushIoBuffers**転送で DMA 中には、キャッシュ操作が不要になりパフォーマンスが低下することができますを実行します。

 

 

 




