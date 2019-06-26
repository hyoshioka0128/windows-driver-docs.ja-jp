---
title: 記憶域クラス ドライバーの ReleaseQueue ルーチン
description: 記憶域クラス ドライバーの ReleaseQueue ルーチン
ms.assetid: 4d0f74f2-6c98-4de1-bc28-dfff3c01e319
keywords:
- ReleaseQueue
- キューの WDK ストレージ
- キューの WDK 記憶域を固定します。
- 固定されたキュー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dc978b236bd1c3afc8ffb7fdc17540d7216d293
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368888"
---
# <a name="storage-class-drivers-releasequeue-routine"></a>記憶域クラス ドライバーの ReleaseQueue ルーチン


## <span id="ddk_storage_class_drivers_releasequeue_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_RELEASEQUEUE_ROUTINE_KG"></span>


ストレージ クラス ドライバー Or しない限り、 **SrbFlags** SRB の特定の要求に対して\_フラグ\_いいえ\_キュー\_凍結し、システム ポートのドライバーで、後に指定された論理ユニットのキューがフリーズします。次のいずれか:

-   論理ユニットは、要求を実行していたバスのリセットが発生しました。

-   論理ユニットに返される SCSISTAT\_確認\_条件または SCSISTAT\_コマンド\_で SRB のクラス ドライバーを見つけることができる終了**ScsiStatus**メンバー。

-   要求がタイムアウトしました。

-   SCSIMESS などのバス メッセージ コマンドによって要求が終了した\_を中止します。

ポートのドライバーでは、SRB の要求を返すことによって、LU 固有のキューを凍結されていることを示します\_状態\_キュー\_固定されている、 **SrbStatus**メンバー。 クラス ドライバーからの新しい要求は、キューに挿入できますが、そのキューが固定されている限り、論理ユニットに autosense 要求のみが送信されます。

各記憶域クラス ドライバーを他のキューに入れられたジョブが実行される前に、エラーを分析する機会が与えられますこれらの条件下でキューを保持します。 たとえば、キューに置かれたジョブは、メディアが変更された場合にキャンセルする必要があります。 キューをフラッシュするドライバーが要求を送信できます、 **SrbFlags** SRB に\_フラグ\_バイパス\_FROZEN\_キュー。

A *ReleaseQueue*日常的な割り当てや IRP と、SRB リリースまたは保持されているキューをフラッシュのいずれかに設定します。 **関数**SRB に、SRB のメンバーを設定する必要があります\_関数\_リリース\_キューまたは SRB\_関数\_フラッシュ\_キュー両方を解放します。保持されているキューとキャンセル中のすべてのキューに要求ターゲット論理ユニットです。 ポートのドライバーをフラッシュ キュー内のすべての要求が完了すると、 **SrbStatus** SRB にメンバーが設定\_状態\_要求\_フラッシュされました。

保持されているキューの解放に失敗により、デバイスは、アクセスできないため、ドライバーの*ReleaseQueue*がメモリ不足の状態であっても成功するルーチンを設計する必要があります。 A *ReleaseQueue*ルーチンを呼び出すことによって、SRB のメモリの割り当てに試みる必要がある最初[ **ExAllocatePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepool)で、 **NonPagedPool**メモリを入力し、その割り当てに失敗した場合をドライバーの初期化中に事前に割り当てられますが、SRB を使用します。 場合は、ドライバーの割り当て」の説明に従って、デバイスの拡張機能の初期化時に予約で保持するために、SRB[デバイス拡張機能の設定を記憶域クラス ドライバーの](setting-up-a-storage-class-driver-s-device-extension.md)その*ReleaseQueue*場合、その SRB を使用できます、同時リリースの複数の操作に必要な場合は、メモリ プールが低く、適切な同期メカニズムです。

なおクラス ドライバーの*ReleaseQueue*ルーチンは、非同期的に呼び出されますから通常その*IoCompletion*ルーチン。 クラス ドライバーの*IoCompletion*ルーチンを呼び出すことはできません*ReleaseQueue*が固定されているキューをフラッシュします。 ただし、呼び出すことができます*ReleaseQueue*単に、固定されていないキュー、およびポートのドライバーをリリースするこのような要求は無視されます。

 

 




