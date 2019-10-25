---
title: 記憶域クラス ドライバーの ReleaseQueue ルーチン
description: 記憶域クラス ドライバーの ReleaseQueue ルーチン
ms.assetid: 4d0f74f2-6c98-4de1-bc28-dfff3c01e319
keywords:
- ReleaseQueue
- WDK ストレージをキューに格納する
- キューの固定 WDK ストレージ
- 固定キューの WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ecd9c93fef7e85afb649fa6f1c346e0ed4bd79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845629"
---
# <a name="storage-class-drivers-releasequeue-routine"></a>記憶域クラス ドライバーの ReleaseQueue ルーチン


## <span id="ddk_storage_class_drivers_releasequeue_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RELEASEQUEUE_ROUTINE_KG"></span>


ストレージクラスドライバーが、指定された要求に対して SRB\_**フラグを使用**しない場合\_\_キュー\_フリーズしていない場合は、次のいずれかの後に、システムポートドライバーによって特定の論理ユニットのキューが凍結されます。:

-   論理ユニットが要求を実行中にバスのリセットが発生しました。

-   論理ユニットは、SCSISTAT\_CHECK\_CONDITION または SCSISTAT\_コマンドを返しました\_終了しました。これは、クラスドライバーが SRB の**ScsiStatus**メンバーで見つけることができます。

-   要求がタイムアウトしました。

-   SCシム ESS\_ABORT などのバスメッセージコマンドによって、要求が終了されました。

ポートドライバーは、SRB\_STATUS\_QUEUE\_の要求を**Srbstatus**メンバーに保持して、LU 固有のキューが固定されていることを示します。 クラスドライバーからの新しい要求はキューに挿入できますが、キューが固定されている間は、自動検出要求だけが論理ユニットに送信されます。

これらの条件下でキューを固定すると、各ストレージクラスドライバーは、他のキューに置かれたジョブが実行される前にエラーを分析する機会を与えます。 たとえば、メディアが変更された場合、キューに登録されたジョブをキャンセルする必要がある場合があります。 キューをフラッシュするには、ドライバーは、固定された\_キュー\_バイパス\_、SRB\_フラグと共に**Srbflags**を使用して要求を送信できます。

*Releasequeue*ルーチンは、凍結されたキューを解放またはフラッシュするために、IRP と SRB を割り当てて設定します。 SRB の**関数**メンバーを SRB\_関数\_RELEASE\_queue または SRB\_\_function に設定する必要があります。これにより、キューに固定されたキューが解放され、ターゲットに対する現在キューに置かれているすべての要求が取り消されます。論理ユニット。 ポートドライバーは、 **Srbstatus**メンバーが SRB に設定されている、フラッシュされたキュー内のすべての要求を完了\_状態\_要求\_フラッシュします。

凍結されたキューを解放できないと、デバイスにアクセスできなくなります。そのため、ドライバーの*releasequeue*ルーチンは、メモリ不足の状態でも成功するように設計する必要があります。 *Releasequeue*ルーチンは、まず**NonPagedPool**メモリ型で[**exallocatepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)を呼び出して SRB にメモリを割り当てようとします。割り当てが失敗した場合は、ドライバーの初期化中に事前に割り当てられた SRB を使用します。 「[ストレージクラスドライバーのデバイス拡張機能の設定](setting-up-a-storage-class-driver-s-device-extension.md)」で説明されているように、ドライバーがデバイス拡張機能を初期化するときに予約に保持する SRB を割り当てる場合、その*releasequeue*は、メモリプールが少ない場合にその SRB を使用できます。複数の同時リリース操作が必要な場合の同期メカニズム。

クラスドライバーの*Releasequeue*ルーチンは、通常、 *iocompletion*ルーチンから非同期的に呼び出されることに注意してください。 クラスドライバーの*Iocompletion*ルーチンは、固定されていないキューをフラッシュするために*releasequeue*を呼び出すことはできません。 ただし、 *Releasequeue*を呼び出して、凍結されていないキューを解放することができ、ポートドライバーは単純にこのような要求を無視します。

 

 




