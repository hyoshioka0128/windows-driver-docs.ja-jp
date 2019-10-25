---
title: ユーザー操作の要求
description: ユーザー操作の要求
ms.assetid: 888faeb0-1984-4b0f-b955-2772a6bd86f7
keywords:
- ユーザー操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- ユーザーとの対話を要求する WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44727dd666614d411c3274b8effa3eee127bf2ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842035"
---
# <a name="requesting-user-interaction"></a>ユーザー操作の要求




 

[*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)を呼び出すと、いつでも、IHV 拡張 DLL は、 [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)関数を呼び出すことによってユーザーとの対話を要求できます。 オペレーティングシステムは、すべてのユーザー操作要求を IHV UI 拡張 DLL に転送します。これにより、要求が処理され、ユーザーに適切なユーザーインターフェイス (UI) ページが表示されます。

要求が完了すると、オペレーティングシステムは[*Dot11ExtIhvProcessUIResponse*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)関数を呼び出して、ユーザーの操作のために IHV UI 拡張 DLL から結果を転送します。 IHV UI 拡張 DLL の詳細については、「[ネイティブ 802.11 IHV Ui EXTENSIONS dll](native-802-11-ihv-ui-extensions-dll2.md)」を参照してください。

たとえば、IHV 拡張 DLL は、次のいずれかの操作をユーザーに要求できます。

-   前または後の関連付け操作の段階についてユーザーに通知します。

-   関連付け後の操作中に認証用の資格情報を入力するようにユーザーに要求します。

[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)関数を呼び出すと、IHV 拡張 DLL は[**DOT11EXT\_ihv\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造へのポインターを*pihvuirequest*パラメーターに渡します。 DOT11EXT\_IHV\_UI\_要求構造では、グローバル一意識別子 (GUID) などの要求を指定します。これにより、UI 要求と、この要求を処理するターゲット UI ページの COM クラス ID (CLSID) が識別されます。

IHV UI 拡張 DLL がユーザー通知を完了すると、オペレーティングシステムは[*Dot11ExtIhvProcessUIResponse*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)関数を呼び出します。 ユーザーが通知を使用してデータを入力した場合、オペレーティングシステムは、データを含むバッファーへのポインターを*Pvresponsebuffer*パラメーターに渡します。

オペレーティングシステムは、保留中の通知要求の状態を定期的に照会する場合があります。 この場合、オペレーティングシステムは[*Dot11ExtIhvIsUIRequestPending*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)を呼び出し、UI 要求の GUID を*guidUIRequest*パラメーターに渡します。

[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)を呼び出す場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   IHV 拡張 DLL では、 [**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)への呼び出しをシリアル化する必要はありません。 DLL には、一度に複数の保留中の UI 要求を含めることができます。

-   特定の GUID の UI 要求は、その GUID に対して[*Dot11ExtIhvProcessUIResponse*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)が呼び出された場合にのみ完了します。 この場合、 *Dot11ExtIhvProcessUIResponse*が呼び出されるまで、IHV 拡張 DLL は、UI 要求に割り当てられたリソースを解放することはできません。

-   保留中のすべての UI 要求は、 [*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)または[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)が呼び出されるたびに取り消されます。 *Ueventtype*パラメーターを WTS\_SESSION\_LOGOFF に設定して[*Dot11ExtIhvProcessSessionChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change)を呼び出すと、保留中のすべての UI 要求も取り消されます。

    このような状況では、IHV 拡張 DLL は、保留中の UI 要求ごとに割り当てられたすべてのリソースを解放する必要があります。

基本サービスセット (BSS) ネットワークの接続状態が変化するたびに、オペレーティングシステムはユーザーとの対話を開始できます。 この場合、オペレーティングシステムは[*Dot11ExtIhvQueryUIRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)関数を呼び出します。 IHV Extensions DLL は、バッファーを割り当て、 [**DOT11EXT\_IHV\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造体としてフォーマットします。 DLL は、接続状態の変更に適した UI ページを参照するように、DOT11EXT\_IHV\_UI\_要求構造体のメンバーを設定します。 オペレーティングシステムは、UI ページを表示する役割を担います。

IHV 拡張  は、 [**Dot11ExtAllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_allocate_buffer)を介して、 [**DOT11EXT\_ihv\_UI\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)構造を含むバッファーを割り当てる必要がある**ことに注意**してください。 DLL は、 [*Dot11ExtIhvQueryUIRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)から復帰した後にバッファーを解放しないようにする必要があります。

 

 

 





