---
title: ユーザーの介入を要求します。
description: ユーザーの介入を要求します。
ms.assetid: 888faeb0-1984-4b0f-b955-2772a6bd86f7
keywords:
- ユーザーの介入 WDK ネイティブ 802.11 IHV 拡張 DLL
- 要求元ユーザーの介入 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2fe595483b2b03c5e16354a0963cc68aea85b80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530218"
---
# <a name="requesting-user-interaction"></a>ユーザーの介入を要求します。




 

呼び出した後、いつでも[ *Dot11ExtIhvInitAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff547469)、IHV 拡張機能の DLL は呼び出すことによって、ユーザーとの対話を要求することができます、 [ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)関数。 オペレーティング システムでは、IHV UI 拡張 DLL は、要求を処理し、ユーザーに適切なユーザー インターフェイス (UI) のページを表示するにすべてのユーザーの操作要求を転送します。

要求が完了したとき、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)ユーザーとの対話の IHV UI 拡張機能の DLL からの結果を転送する関数。 IHV UI 拡張機能の DLL の詳細については、[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)を参照してください。

たとえば、IHV 拡張機能の DLL は、次のいずれかのユーザーの操作を要求できます。

-   前または後のアソシエーションの操作の段階についてユーザーに通知します。

-   認証後の関連付け操作中に自分の資格情報の入力を求めます。

呼び出し時に、 [ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)関数へのポインターを渡します IHV 拡張機能の DLL を[ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)構造体を*pIhvUIRequest*パラメーター。 DOT11EXT\_IHV\_UI\_構造など、グローバルに一意な ID (GUID)、COM と同様に、UI 要求を識別する要求を指定する要求クラスのこの要求を処理する対象の UI ページの ID (CLSID)。

IHV UI 拡張機能の DLL には、ユーザー通知が完了したら、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504)関数。 オペレーティング システムには、データを格納するバッファーへのポインターを渡します通知を通じて任意のデータを入力した場合、 *pvResponseBuffer*パラメーター。

オペレーティング システムでは、保留中の通知要求の状態を定期的にクエリがあります。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvIsUIRequestPending* ](https://msdn.microsoft.com/library/windows/hardware/ff547479) UI 要求の GUID を渡すと、 *guidUIRequest*パラメーター。

呼び出すときに[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)、IHV 拡張機能の DLL が次のガイドラインに従う必要があります。

-   IHV 拡張機能の DLL がへの呼び出しをシリアル化する必要はありません[ **Dot11ExtSendUIRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547567)します。 DLL は、いつでも 1 つ以上の保留中の UI の要求でことができます。

-   特定の GUID の UI の要求が完了した場合にのみ[ *Dot11ExtIhvProcessUIResponse* ](https://msdn.microsoft.com/library/windows/hardware/ff547504) GUID が呼び出されます。 このような状況で IHV 拡張機能の DLL を解放しないようにまで UI 要求に割り当てられたリソース*Dot11ExtIhvProcessUIResponse*が呼び出されます。

-   UI 保留中のすべての要求が取り消されたときに[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)または[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)が呼び出されます。 要求は取り消されますも保留中のすべての UI たびに[ *Dot11ExtIhvProcessSessionChange* ](https://msdn.microsoft.com/library/windows/hardware/ff547501)を呼び出すと、 *uEventType*パラメーター WTS に設定\_セッション\_ログオフします。

    このような場合は、IHV 拡張機能の DLL は、保留中の UI 要求ごとに割り当てられているすべてのリソースを解放する必要があります。

オペレーティング システムは、基本的なサービスに接続状態の変更が (BSS) ネットワークを設定するたびに、ユーザーの相互作用自体を開始できます。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvQueryUIRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff547507)関数。 IHV 拡張機能の DLL を選択し、バッファーを割り当てますとして書式設定、 [ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)構造体。 DLL、DOT11EXT のメンバーを設定する\_IHV\_UI\_ページの UI を参照する構造体の要求が接続状態の変更に適してします。 オペレーティング システムは、UI のページを表示します。

**注**  IHV 拡張機能を含むバッファーを割り当てる必要があります、 [ **DOT11EXT\_IHV\_UI\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff547637)構造体を通じて[ **Dot11ExtAllocateBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff547419)します。 DLL から返された後、バッファーを解放する必要がありますいない[ *Dot11ExtIhvQueryUIRequest*](https://msdn.microsoft.com/library/windows/hardware/ff547507)します。

 

 

 





