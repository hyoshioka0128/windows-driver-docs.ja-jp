---
title: 特定のアロケーターのフィルター処理
description: 特定のアロケーターのフィルター処理
ms.assetid: 581f3000-4e66-4ba0-979d-b187115a30b2
keywords:
- 特定のアロケーター WDK カーネルストリーミングをフィルター処理する
- フィルターアロケーター WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b2dac1763825a42d6ab31b17452bf67405e324a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834389"
---
# <a name="filter-specific-allocators"></a>特定のアロケーターのフィルター処理





オンボードメモリまたはその他のデバイスに依存するストレージメソッドにアロケーターを必要とするフィルターは、アロケーターの[プロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)と[メソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)をサポートすることによって特定のアロケーターを提供できます。 詳細については、「 [**Ksk プロパティ\_STREAM\_アロケーター**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)」を参照してください。

フィルターは、\_IRP のフレームオプションを指定する\_型 KSK CREATE\_要求\_アロケーターの MJ を受け取ります。 ミニドライバーのアロケーター作成ルーチンは、 [**KsValidateAllocatorCreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksvalidateallocatorcreaterequest)を呼び出して作成要求を検証します。 呼び出しが成功した場合、このルーチンは関連する[**Ksallocator\_フレーミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)構造体へのポインターを返します。

フィルターがフレームの要件を満たすことができない場合、IRP に応答してエラーコードが返されます。 それ以外の場合、フィルターは構造体へのポインターをファイルオブジェクトの**Fscontext**メンバーにアタッチし、結果として得られるアロケーター要求を処理します。

ストリーミングインターフェイスに渡されたバッファーをフィルターによってインプレースで変更する必要がある場合、ユーザーモードクライアントは、関連する[**ksallocator\_フレーミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)で ksallocator\_REQUIREMENTF\_インプレース\_MODIFIER フラグを設定します。データ.

アロケーターに使用できるインターフェイスは2つあります。 まず、すべてのアロケーターは、IRP ベースの[Ksk Methodsetid\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)をサポートする必要があります。 このメカニズムを使用するアロケーターは、割り当てられたフレームの最大数に制限されています。 この制限を超えてフレームを割り当てる要求は、保留中とマークされます。

次に、ミニドライバーは、割り当てプールの種類をディスパッチ\_レベルで処理できる場合、関数テーブルへのアクセスをサポートできます。 関数テーブルへのアクセスの提供は省略可能です。 これを行うには、 [Kspropsetid\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)のプロパティをサポートします。

ディスパッチ\_レベルのインターフェイスは、次のように動作します。

割り当て要求がアロケーターに送信されると、アロケーターは、使用可能な場合はフレームへのポインターを返します。 そうでない場合は、直ちに**NULL**が返されます。

解放要求がアロケーターに送信されると、アロケーターは、解放されたフレームが使用可能であることをクライアントに通知するストリームアロケーター "free frame" イベントを通知します。 また、完了を待機している割り当て要求の Irp がある場合は、アロケーターがワーカー項目をスケジュールする必要があります (現在の IRQL がパッシブ\_レベルでない場合)。その後、解放フレームで要求を完了します。

ディスパッチ\_レベルのインターフェイスと、IRP ベースのインターフェイスの両方が、空きフレームに対して競合する可能性があります。 KS は、このキューをキャンセルスピンロックを使用して同期します。

 

 




