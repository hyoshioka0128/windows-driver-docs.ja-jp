---
title: VM キューの割り当て
description: VM キューの割り当て
ms.assetid: 2645a6e5-3824-469c-84d5-8e49fa01f494
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e72a7e6a3ad280ce51e5bfb5774a6f7f8683925f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578104"
---
# <a name="allocating-a-vm-queue"></a>VM キューの割り当て





上位のドライバーの問題、初期構成パラメーターのセットを持つキューを割り当てるには、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569784)メソッド要求の OID。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造体。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 **NDIS\_受信\_キュー\_パラメーター**新しいキューの id と、MSI X テーブルのエントリを持つ構造体。

[ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)で構造が使用される、 [OID\_受信\_フィルター\_割り当てる\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569784) OID と[OID\_受信\_フィルター\_キュー\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569794) OID。 VM キュー パラメーターの詳細については、[VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)を参照してください。

上にあるドライバーを初期化します、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)次のキュー構成パラメーターを含む構造体。

-   キューの種類 (**NdisReceiveQueueTypeVMQueue**から、 [ **NDIS\_受信\_キュー\_型**](https://msdn.microsoft.com/library/windows/hardware/ff567217)列挙します)。

-   キューのプロセッサの関係。

-   キュー名と仮想マシンの名前。

-   先読み分割パラメーター。

    **注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。

     

**注**  上にあるドライバーは、NDIS を設定できる\_受信\_キュー\_パラメーター\_1 秒あたり\_キュー\_受信\_を示す値とNDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_で必須フラグ、**フラグ**のメンバー[ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造体。 その他のフラグは、キューの割り当ては使用されません。

 

NDIS は、受信キューを割り当てる OID 要求を受信、キューのパラメーターを確認します。 NDIS は、必要なリソースとキューの id を割り当て後、は、基になるミニポート ドライバーに OID 要求を送信します。 キューの id は、関連付けられているネットワーク アダプターに固有です。

ミニポート ドライバーは、受信キューに、必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に場合、に、成功のステータスの OID 要求を完了します。

NDIS がキュー識別子を割り当てます NDIS ミニポート ドライバーに OID 要求を送信する前に、 **QueueId**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造体であり、ミニポート ドライバーにメソッド要求を渡します。 ミニポート ドライバー MSI X テーブルのエントリを提供する、 **MSIXTableEntry**メンバー。

ミニポート ドライバーでは、割り当てられた受信キューのキューの識別子を保持する必要があります。 NDIS は、ミニポート ドライバーに後続の呼び出しの受信キューのキューの id を使用して受信キューで受信フィルターを設定、受信キュー パラメーターを変更または無料の受信キュー。

**注**  既定のキュー (キューの id 0) が常に割り当てられ、解放することはできません。

 

上にあるドライバーは、キュー パラメーターを変更またはキューを解放するなど、NDIS が提供、OID の後続の要求でキューの id を使用する必要があります。 キューの id はすべての OOB データにも含まれています。 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)キューに関連付けられている構造体。 ドライバーを使用して、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407) NETでキューのidを取得するマクロ\_バッファー\_リスト構造体。

**注**  プロトコル ドライバーは、キューが正常に割り当てられ、キューが削除される前に、いつでもの VMQ フィルターを設定できます。

 

プロトコル ドライバーの問題、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)メソッド OID 要求のキューの割り当てを完了します。 割り当てが完了すると、ミニポート ドライバーは共有メモリおよびその他のリソースを割り当てることができます。 共有メモリ リソース割り当ての詳細については、[共有メモリ リソース割り当て](shared-memory-resource-allocation.md)を参照してください。

ミニポート後は、ドライバーは OID を受け取ります。\_受信\_フィルター\_キュー\_割り当て OID 要求とハンドルが正常にキュー内にある、 *Allocated*状態。 キューの状態の詳細については、[キューの状態と操作](queue-states-and-operations.md)を参照してください。

これを発行する必要があります、上にあるドライバーを割り当てる後、1 つまたは複数のキューの受信 (および必要に応じて、最初のフィルターを設定) [OID\_受信\_フィルター\_キュー\_割り当て\_完全な](https://msdn.microsoft.com/library/windows/hardware/ff569793)割り当てが受信キューの現在のバッチの完了したミニポート ドライバーに通知する OID 要求を設定します。

フィルターがそのキューに設定されていない場合、ミニポート ドライバーは受信キュー内のすべてのパケットを保持する必要があります。 キューのなかった、フィルターを設定またはすべてのフィルターをクリア、キューを空にする必要があり、すべてのパケットを破棄する必要があります。 ドライバー スタックを示されたまたは、キューに保持されますができません。

後続のドライバーが使用、 [OID\_受信\_フィルター\_FREE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569789) OID を割り当て、キューを解放します。 キューを解放する方法の詳細については、[VM キューの解放](freeing-a-vm-queue.md)を参照してください。

 

 





