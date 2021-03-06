---
title: 特定のアロケーターのフィルター処理
description: 特定のアロケーターのフィルター処理
ms.assetid: 581f3000-4e66-4ba0-979d-b187115a30b2
keywords:
- 特定のアロケーター WDK カーネルのストリーミングをフィルター処理します。
- フィルターのアロケーターの WDK カーネルがストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da2183f14a73a53e33369adb37aa5852a44d33a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384055"
---
# <a name="filter-specific-allocators"></a>特定のアロケーターのフィルター処理





オンボード メモリやその他のデバイスの依存するストレージ メソッドのアロケーターを必要とするフィルターは、アロケーターをサポートすることで特定のアロケーターを提供できます[プロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)と[メソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)します。 詳細については、次を参照してください。 [ **KSPROPERTY\_ストリーム\_アロケーター**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)します。

フィルターは IRP を受信\_MJ\_KSCREATE の種類の作成\_要求\_アロケーターは、アロケーターのフレームのオプションを指定します。 ミニドライバーのアロケーター作成ルーチンを呼び出して、要求の作成を検証する[ **KsValidateAllocatorCreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksvalidateallocatorcreaterequest)します。 このルーチンが、関連するへのポインターを返します、呼び出しが成功した場合[ **KSALLOCATOR\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)構造体。

フィルターは、フレームの要件を満たすことができない、IRP への応答でエラー コードが返されます。 それ以外の場合、フィルターを構造体へのポインターを接続、 **FsContext**ファイル オブジェクトおよびサービスのメンバーの結果として得られるアロケーターを要求します。

渡されたバッファーの場合は、ストリーミング インターフェイスを変更する必要がありますインプレースでのフィルターによって、ユーザー モードのクライアント設定、KSALLOCATOR\_REQUIREMENTF\_インプレース\_に関連する修飾子フラグ[ **KSALLOCATOR\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)構造体。

2 つのインターフェイスは、アロケーター使用できます。 最初に、すべてのアロケーターは IRP ベースをサポートする必要があります[KSMETHODSETID\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-streamallocator)します。 このメカニズムを使用するアロケーターは、割り当て済みのフレームの最大数に制限されます。 この制限を超えるフレームの割り当てを要求は保留中のマークにされます。

次に、ミニドライバー アクセスをサポートできます関数テーブル ディスパッチでプールの割り当ての種類が処理される場合\_レベル。 関数のテーブル アクセスの提供は省略可能です。 これには、プロパティをサポートしている、 [KSPROPSETID\_StreamAllocator](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-streamallocator)します。

ディスパッチ\_レベルのインターフェイスは次のように動作します。

アロケーターに、割り当て要求が送信されると、アロケーターは 1 つが使用可能な場合は、フレームにポインターを返します。 すぐに返されたそうでない場合は**NULL**します。

アロケーターに無料の要求が送信されると、アロケーターは、無料のフレームが使用できることをクライアントに通知するストリーム アロケーター「無料フレーム」イベントを通知します。 さらに、割り当て要求の Irp の完了を待機している、アロケーターは、作業項目をスケジュールする必要がある場合 (現在の IRQL がパッシブでない場合\_レベル) および無料のフレームを使用して要求を完了します。

両方のディスパッチ\_レベルのインターフェイスとフレームを無料 IRP ベースのインターフェイス。 KS では、キャンセルのスピン ロックを使用して、このキューを同期します。

 

 




