---
title: ストリーム クラス ミニドライバーの作成に関する注意事項
description: ストリーム クラス ミニドライバーの作成に関する注意事項
ms.assetid: dc966b47-4ffe-4122-847d-118a465bf5f5
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、書き込み
- streaming ミニドライバー WDK Windows 2000 カーネル、書き込み
- ミニドライバー WDK Windows 2000 カーネルストリーミング、書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff26c752670f79f7c7e8a9f3153eddcb95596e0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823592"
---
# <a name="notes-on-writing-stream-class-minidrivers"></a>ストリーム クラス ミニドライバーの作成に関する注意事項





-   ミニドライバーは Intel と Intel 以外の両方の x86 プロセッサで実行する必要があるため、C (またはその他の高水準言語) で記述する必要があります。 ミニドライバーにアセンブリ言語のソースコードを含めることはできません。

-   一部のハードウェアでは、機能する前にファームウェアを読み込む必要があります。 ミニドライバーは、ミニドライバーのデータセグメントにファームウェアを埋め込む必要があります。 必要に応じて、ミニドライバーは適切な WDM ファイル i/o 関数を呼び出すことによって、ファームウェアを動的に読み込むことができます。たとえば、ミニドライバーでは、埋め込みを行うことができない複数のバージョンのファームウェアを使用する場合などです。

-   ミニドライバーがほとんどの要求に対してパッシブ\_レベル (低優先度) に移行する必要がある場合は、同期をオフにします ( [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造の**TurnOffSynchronization**メンバーを**TRUE**に設定します)。 同期の詳細については、「[ミニドライバー synchronization](minidriver-synchronization.md) 」セクションを参照してください。

-   ハードウェアリソース (ポートまたはメモリアドレス) には、 *wdm*で見つかったマクロを使用してアクセスする必要があります。 たとえば、word のポートに書き込むには、マクロの書き込み\_ポート\_USHORT を使用する必要があります。 ポートにバッファーを書き込むには、\_ポート\_バッファーを書き込み\_USHORT を使用する必要があります。

-   ミニドライバーは、保護されていないスピンループを含むことはできません。 ポートの値が変更されるのを待機している間にミニドライバーがスピンする必要がある場合、ループはループカウンターで保護されている必要があります。

-   短時間にわたって同期的に待機する必要があるミニドライバーは、 [**Kestallexecutionprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor)を使用する必要があります。 システムのパフォーマンスが低下しないように、このルーチンは控えめに使用する必要があります。

-   操作完了のために長時間 (数マイクロ秒以上) 待機する必要があるミニドライバーは、割り込みドリブンであるか、または[**Streamclassscheduletimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassscheduletimer)関数を使用して時間指定のコールバックをスケジュールする必要があります。 ミニドライバーは、システム全体のパフォーマンスを低下させるため、状態の変化を待機するのに数マイクロ秒を超える時間は必要ありません。

-   バスマスタ DMA を使用するデバイスでは、ストリーム要求ブロック構造に指定されたスキャッター/ギャザー DMA リスト ([**HW\_stream\_request\_block**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)) を使用する必要があります。 DMA バッファーのロックまたはマッピングは必要ありません。 詳細については、「ハードウェア\_ストリーム」を参照して **\_ブロック構造\_要求**してください。 さらに、ミニドライバーが DMA 要求を分割する必要がある場合は、 [**StreamClassGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetphysicaladdress)関数を使用して、仮想バッファーポインター内のオフセットの物理アドレスを取得できます。

 

 




