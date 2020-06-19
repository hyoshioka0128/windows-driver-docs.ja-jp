---
title: AVStream のパケットベースの DMA
description: AVStream のパケットベースの DMA
ms.assetid: 4246819e-d8d6-4302-9477-675ca181b1e3
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA サービス WDK AVStream
- ダイレクトメモリアクセス WDK AVStream
- パケットベースの DMA WDK AVStream
- スキャッター/ギャザー DMA WDK AVStream
- キャプチャバッファー WDK AVStream
- WDK AVStream のバッファー
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: bef08ab666d32027fbd08ad91e105aa9ed5cf1e7
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073435"
---
# <a name="packet-based-dma-in-avstream"></a>AVStream のパケットベースの DMA

パケットベースのダイレクトメモリアクセス (DMA) は、ミニドライバーがから直接データを読み取り、ユーザーモードから受信したバッファーをキャプチャするために直接データを書き込む場合に発生します。 Windows Driver Kit (WDK) サンプルの[Avstream シミュレートされたハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)は、この種類の DMA を実行する avstream ミニドライバーを構築する方法を示しています。

パケットベースの DMA スキームを実装するには、次のようにします。

1. KSPIN フラグを指定する \_ \_ \_ と、関連する[**kspin \_ DESCRIPTOR \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**Flags**メンバーにマッピングが生成されます。 このフラグは、スキャッター/ギャザーサポートを備えたバスマスターでのみ使用する必要があることに注意してください。

1. 「[ハードウェアの AVStream ミニドライバーの作成](writing-avstream-minidrivers-for-hardware.md)」の説明に従って、interrupt service ルーチン (ISR) を登録します。

次に、 [*Avstrminidevicestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicepnpstart)のディスパッチで、次のようにします。

1. [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を使用して DMA アダプターオブジェクトを設定します。

1. [**KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)を呼び出して、AVSTREAM に DMA アダプターオブジェクトを登録します。

ミニドライバーは、 [**KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdeviceregisteradapterobject)への呼び出しに*MaxMappingByteCount*パラメーターを指定することで、単一のスキャッター/ギャザーマッピングの最大サイズを指定します。

スキャッター/ギャザーマッピングがこの最大サイズを超えると、AVStream は自動的に複数のスキャッター/ギャザーマッピングにマッピングを解除します。各マッピングは、 *MaxMappingByteCount*で指定されたサイズを超えません。

[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバックルーチンも指定する必要があります。 ドライバーライターは、このコールバックに適した機能を選択する必要があります。 1つの例として、次の操作を行うことができます。

1. [**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出します。

1. [**Ksk ストリームポインター複製**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)を呼び出して、先頭のエッジを複製します。

1. 複製に基づくプログラム DMA ハードウェア。

1. [**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)または[**ksstreamポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvance)を呼び出して、最先端を進めます。

1. 必要に応じて、手順 2. を繰り返します。

ハードウェアが DMA の完了に割り込むと、カーネルは、ベンダーが以前に登録した ISR を呼び出します。 ISR では、ミニドライバーは遅延プロシージャ呼び出し (DPC) をキューに置いています。

DPC は、 [**Ksk ストリーム \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造の**dataused**と他のメンバーを更新する必要があります。 DPC は、次に、 [**Ksstreamポインター delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)を呼び出して、複製を削除し、関連付けられているフレームを解放します。

また、フレームの一部だけが完了している場合は、DPC が複製ポインターを進める可能性もあります。 これを行うには、 [**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)を呼び出します。

処理を再開する必要がある場合は、 [**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)を呼び出します。

> [!NOTE]
> マッピングの長さが1ページ未満の場合、1つの物理ページに存在することは保証されません。
