---
title: PnP ページング要求の処理
description: PnP ページング要求の処理
ms.assetid: c30c70d9-69c6-42d7-ae69-9c2421ba1d53
keywords:
- 記憶域フィルター ドライバー WDK、PnP
- フィルター ドライバー WDK の記憶域、PnP
- SFD WDK の記憶域、PnP
- PnP WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15721b5b747f14fbc7a606863f24f5294d811774
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527501"
---
# <a name="handling-pnp-paging-requests"></a>PnP ページング要求の処理


## <span id="ddk_handling_pnp_paging_requests_kg"></span><span id="DDK_HANDLING_PNP_PAGING_REQUESTS_KG"></span>


ストレージのフィルター ドライバーは PnP ページング要求を処理する必要があります ([**IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)で[ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)と**Parameters.UsageNotification.Type**設定**DeviceUsageTypePaging**) 場合これがフィルター処理関数のドライバーでは、この IRP を処理します。

次の項目は、フィルターは DeviceExtension に追加する必要があります。

ULONG PagingCount;

KEVENT PagingCountEvent;

記憶域フィルター ドライバーの PnP ページング要求を受信すると、PagingCount との設定は、更新する必要があります、**は\_POWER\_PAGABLE**ビットで、フィルター操作を行います。 更新のタイミング、**は\_POWER\_PAGABLE**ビットがビットがされているかどうかに依存設定、またはクリアします。 ビットを設定する必要があります、そのフィルター ドライバーが設定する必要があります、IRP が示された場合*する前に*IRP がドライバー スタックを転送します。 ビットがクリアする必要があります、IRP が示す場合は、フィルター ドライバーがすぐにビットを消去しないでください。 、IRP を転送し、それらの状態を返すし、下位のドライバーを返す場合にのみ、ビットをオフにする下位のドライバーを待つ必要があります最初**状態\_成功**します。

次に、記憶域フィルター ドライバーによって実行されたアクションのフローをトレースします。 C コードのアウトラインを表示するためのアウトラインのすぐ下にある擬似コード サンプルを参照してください。

A. デバイスが起動したことを確認します。 そうでない場合は失敗し、**状態\_デバイス\_いない\_準備**。

B. PagingCountEvent (kewaitforsingleobject の 1 (PagingCountEvent、...)) に同期します。

C. 最後のページングのデバイスを削除する場合 ((! **Parameters.UsageNotification.InPath** && (PagingCount == 1) ) then
1.  ローカルのブール値に設定**TRUE**と

2.  場合、**は\_POWER\_突入**ビットがないフィルターで設定し、設定、**は\_POWER\_PAGABLE**ビット。

    理由は、次の**は\_POWER\_PAGABLE**ビット方向では、方法ではなくよう設定します。

    電源状態をいずれかのデバイス オブジェクトのセットを下げる場合、**は\_POWER\_PAGABLE** bit より高度なドライバーをすべて行う必要があります、同じです。 フィルター ドライバーは、設定が失敗した場合、**は\_POWER\_PAGABLE**下位のスタックのページング要求 IRP を送信する前に bit で、そのことがこの条件に違反次のように。

    フィルター ドライバーを設定しないと、**は\_POWER\_PAGABLE**をその下にあるドライバー スタックのドライバーにページング要求 IRP を転送する前にそのフィルターにビットします。 たとえば次に、下位のドライバーが設定、**は\_POWER\_PAGABLE**独自 do ビットします。 最後とを IRP の完了する前に、フィルター ドライバー IRP が発生した電源でします。 その時点で、**は\_POWER\_PAGABLE**ビットでフィルターをクリアするは、下位レベルのドライバーの操作を実行、システムのクラッシュの原因で設定されます。

    設定するのには安全では、**は\_POWER\_PAGABLE**フィルター ドライバーのデバイス、およびページングがなくなるため I/O のアクティブなページング ファイルがなくなったため、下位のスタックでは、ページング要求を転送する前に bitこれで発生します。 このページング ファイルを削除する要求が成功すると、フィルター ドライバーは行われます。 フィルター ドライバーが単にオフにすると、フラグの元の状態を復元できます要求に失敗した場合、**は\_POWER\_PAGABLE** IRP を完了する前にビットします。 ページング ファイルの要求がシリアル化されるため、他のスレッドが変更ことこのビット フィルター ドライバー最後変更されるため危険はありません。

D。 同期的に下位のドライバーに IRP を転送します。

E を押します。 IRP が正常に完了し、場合

1.  IoAdjustPagingPathCount を呼び出す (& PagingCount、 **Parameters.UsageNotification.InPath**) をインクリメントまたはデクリメント、PagingCount にします。 IoAdjustPagingPathCount では、InterlockedIncrement またはの値によって PagingCount InterlockedDecrement **Parameters.UsageNotification.InPath**します。 値**TRUE**ページング ファイルが追加されること、そのインクリメントを示します、PagingCount; の値**FALSE**ページング ファイルがされていることを示します、PagingCount をデクリメントので削除します。

2.  場合**Parameters.UsageNotification.InPath**は**TRUE**、ページング ファイルが追加されたチェック ボックスをオフようにされている、**は\_POWER\_PAGABLE**ビット。

F です。 それ以外の場合、IRP が失敗します。

1.  ローカルのブール値かどうかを確認してください**は\_POWER\_PAGABLE**の方法では、フィルターの実行で設定されました。

2.  場合**は\_POWER\_PAGABLE**された方法でセットをスケール ダウン、オフにします。

G です。 最後の同期 (KeSetEvent (PagingCountEvent、...))。

### <a name="span-idpseudocodeexamplespanspan-idpseudocodeexamplespanpseudocode-example"></a><span id="pseudocode_example"></span><span id="PSEUDOCODE_EXAMPLE"></span>擬似コードの例

文字でマークされているセクションでは、(*//A*、 *//B*など) では、上記のアウトラインの文字には、次のコード サンプル マップします。

```cpp
case DeviceUsageTypePaging: { 
    BOOLEAN setPageable = FALSE; 
    BOOLEAN addPageFile = irpStack -> 
                          Parameters.UsageNotification.InPath; 
 
 // A 
    if((addPageFile) && 
        (extension -> CurrentPnpState != 
        IRP_MN_START_DEVICE)) { 
            status = STATUS_DEVICE_NOT_READY; 
            break; 
        } 
 // B 
    KeWaitForSingleObject(&commonExtension -> PagingCountEvent, 
                                    Executive, KernelMode, 
                                    FALSE, NULL); 
 // C 
    if (!addPageFile && commonExtension -> PagingCount == 1 ) { 
        // The last paging file is no longer active.
        // Set the DO_POWER_PAGABLE bit before 
        // forwarding the paging request down the 
        // stack.
        if (!(DeviceObject->Flags & DO_POWER_INRUSH)) { 
            DeviceObject->Flags |=             DO_POWER_PAGABLE; 
            setPageable = TRUE; 
        ) 
    ) 
 // D 
        status = ForwardIrpSynchronous(commonExtension, Irp); 
 // E
        if (NT_SUCCESS(status)) { 
            IoAdjustPagingPathCount(&commonExtension -> PagingCount, 
                                    addPageFile); 
        if (addPageFile && commonExtension -> PagingCount == 1) { 
            // Once the lower device objects have 
            // succeeded the addition of the paging 
            // file, it is illegal to fail the 
            // request. It is also the time to 
            // clear the Filter DO&#39;s 
            //DO_POWER_PAGABLE flag.
 
            DeviceObject->Flags &= ~DO_POWER_PAGABLE; 
            } 
        } else { 
 // F 
        if (setPageable == TRUE) { 
            DeviceObject->Flags &= ~DO_POWER_PAGABLE; 
            setPageable = FALSE; 
        } 
    } 
 // G 
        KeSetEvent(&commonExtension->PagingCountEvent, 
                                    IO_NO_INCREMENT, FALSE); 
                                    break;
    } *Do not use or delete the last paragraph mark. It maintains the template setup and formats.
```

 

 




