---
title: ストリーム クラス ミニドライバーの作成に関する注意事項
description: ストリーム クラス ミニドライバーの作成に関する注意事項
ms.assetid: dc966b47-4ffe-4122-847d-118a465bf5f5
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルでは、書き込み
- ミニドライバー WDK Windows 2000 のカーネルのストリーミング、書き込み
- ミニドライバー WDK Windows 2000 のカーネル ストリーム、書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1d98a59d1a7ec0d56f592433abaace309990f38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377764"
---
# <a name="notes-on-writing-stream-class-minidrivers"></a>ストリーム クラス ミニドライバーの作成に関する注意事項





-   ミニドライバーは、プロセッサでは、Intel と非 Intel x86 の両方で実行する必要があり、C# (またはその他の高級言語) で記述する必要があります。 ミニドライバーは、アセンブリ言語のソース コードを含めることはできません。

-   一部のハードウェアでは、ファームウェアを読み込む前に、機能することが必要です。 ミニドライバーは、ミニドライバーのデータ セグメントのファームウェアを埋め込む必要があります。 必要に応じて、ミニドライバーがなど、ミニドライバーはいくつかのバージョンのファームウェアとなると埋め込むことは実用的でないを使用している場合は、適切な WDM ファイル I/O の関数を呼び出すことによってのファームウェアを動的に読み込むことができます。

-   同期をオフに (設定して、 **TurnOffSynchronization**内のメンバー、 [ **HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff559682) 構造体**TRUE**)、ミニドライバーは、パッシブに移動する必要がある場合\_ほとんど依頼のレベル (低優先度)。 参照してください、[ミニドライバー同期](minidriver-synchronization.md)同期の詳細については、セクション。

-   見つかったマクロを使用するハードウェア リソース (ポートまたはメモリ アドレス) にアクセスする必要があります*wdm.h*します。 たとえば、word のポートに書き込むマクロ記述\_ポート\_USHORT を使用する必要があります。 ポートにバッファーを記述するには記述\_ポート\_バッファー\_USHORT を使用する必要があります。

-   ミニドライバーでスピン ループが保護されないいない必要があります。 ミニドライバーは、変更するポートの値の待機中に迅速に作成する必要があります、ループがループ カウンターによって保護する必要があります。

-   ミニドライバーを小さな一定期間を使用する必要がありますを同期的に待機する必要がある[ **KeStallExecutionProcessor**](https://msdn.microsoft.com/library/windows/hardware/ff553295)します。 システムのパフォーマンスが低下しないようにこのルーチンを控えめに使用する必要があります。

-   ミニドライバーを長期間 (複数のマイクロ秒)、操作が完了するを待機する必要がある必要がある割り込み駆動またはいずれかを使用して、 [ **StreamClassScheduleTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff568264)関数時間指定のコールバックをスケジュールします。 ミニドライバーは、システム全体のパフォーマンスが低下するために、状態の変更の待機している複数のマイクロ秒単位の回転しない必要があります。

-   バス マスター DMA を使用するデバイスでのみストリーム要求のブロック構造体で提供されるスキャッター/ギャザー DMA の一覧を使用する必要があります ([**HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)). ロックまたは DMA バッファーのマッピングは必要ありません。 参照してください、 **HW\_ストリーム\_要求\_ブロック**詳細については、構造体。 さらに、ミニドライバーは、DMA の要求を分割する必要がある場合、 [ **StreamClassGetPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff568247)内の仮想バッファー ポインターのオフセットの物理アドレスを取得する関数を使用できます。

 

 




