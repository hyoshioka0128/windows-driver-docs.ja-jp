---
title: 中間ドライバーのミニポート ドライバーとしての登録
description: 中間ドライバーのミニポート ドライバーとしての登録
ms.assetid: a01bc0f4-4a03-4d44-88c0-7029042d6953
keywords:
- 中間ドライバーの登録
- ドライバー WDK 中級レベルのネットワーク、登録します。
- NDIS 中間ドライバ、WDK を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95393d5e1858ac892b38a77a51f5eb51a510117a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374782"
---
# <a name="registering-an-intermediate-driver-as-a-miniport-driver"></a>中間ドライバーのミニポート ドライバーとしての登録





中間のドライバーは呼び出し[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)をエクスポートするその*MiniportXxx*関数。 *NdisMiniportDriverHandle*によって返される**NdisMRegisterMiniportDriver**中間ドライバーによって保持および NDIS ドライバーを呼び出すときに入力する必要があります[ **NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)します。

中間のドライバーが必要です。

1.  0 に初期化する[ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造体[ **NdisZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiszeromemory).

2.  必須の住所は格納*MiniportXxx*関数、省略可能なあらゆるとして*MiniportXxx*ドライバーをエクスポートする関数。

NDIS 6.0 の機能をサポートする中間のドライバーは、バージョン 6.0 のミニポート ドライバーとして登録する必要があります。 ミニポート ドライバーのバージョン番号を指定する方法については、次を参照してください。 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)します。

次のエントリを設定する必要があります*MiniportCharacteristics*を有効な*MiniportXxx*関数のアドレスでない場合、関数オプションはエクスポートされません。 ドライバーが、関数をエクスポートされない場合は、アドレスを設定**NULL**します。

<a href="" id="setoptionshandler"></a>**SetOptionsHandler**  
[*MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数は省略可能です。 NDIS 呼び出し*MiniportSetOptions*のため中間ドライバーは、省略可能なハンドラーを指定できるようにします。

<a href="" id="initializehandlerex"></a>**InitializeHandlerEx**  
NDIS 呼び出し[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)中間ドライバー呼び出しの結果**NdisIMInitializeDeviceInstanceEx**はミニポート アダプターを初期化するには初期化されている仮想ミニポートの操作。

<a href="" id="halthandlerex"></a>**HaltHandlerEx**  
[*MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)は必要な関数です。 NDIS 呼び出し*MiniportHaltEx*中間ドライバーが公開されているミニポート仮想デバイスが無効または停止している場合、または中間のドライバーが呼び出された場合[ **NdisIMDeInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimdeinitializedeviceinstance)その削除を開始します。

<a href="" id="unloadhandler"></a>**UnloadHandler**  
[*MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)は必要な関数です。 NDIS 呼び出し*MiniportDriverUnload*中間ドライバーをアンロードします。

<a href="" id="pausehandler"></a>**PauseHandler**  
[*MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)は必要な関数です。 NDIS 呼び出し*MiniportPause*中間ドライバーの場合は、指定した仮想ミニポート経由のネットワーク データの流れを停止します。

<a href="" id="restarthandler"></a>**RestartHandler**  
[**MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)は必要な関数です。 NDIS 呼び出し*MiniportRestart*中間ドライバーの場合は、指定した仮想ミニポートを通してネットワーク データのフローが再起動します。

<a href="" id="oidrequesthandler"></a>**OidRequestHandler**  
[*MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request) OID を受け取る\_*XXX*と呼ばれる上位のドライバーから送信された要求[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)または NDIS から。 中間のドライバーは、要求を処理または、基になるミニポート ドライバーに渡す可能性があります。

<a href="" id="sendnetbufferlistshandler"></a>**SendNetBufferListsHandler**  
[*MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)を 1 つまたは複数のポインターの配列を受け取る[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)ネットワークを指定する構造体ネットワーク経由で伝送されるデータ。 すべての中間ドライバーを指定する必要があります、 *MiniportSendNetBufferLists*関数。 詳細については、次を参照してください。[送信ネットワーク データを、中間ドライバー](transmitting-network-data-through-an-intermediate-driver.md)します。

<a href="" id="returnnetbufferlistshandler"></a>**ReturnNetBufferListsHandler**  
[*MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)返された受信[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体に示されていましたが、呼び出すことによってより高度なドライバー **NdisMIndicateReceiveNetBufferLists**します。 呼び出し**NdisMIndicateReceiveNetBufferLists**上位レベルのドライバーに示されるリソースの制御を解放します。 中間のドライバーが NET に割り当てられた後、各を示す値より高度なドライバーが消費する\_バッファー\_をリストの構造とについて説明しますが、リソースが返されます、 *MiniportReturnNetBufferLists*関数。

<a href="" id="cancelsendhandler"></a>**CancelSendHandler**  
[*MiniportCancelSend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_send)は必要な関数です。 NDIS 呼び出し*MiniportCancelSend*送信要求を取り消します。

<a href="" id="checkforhanghandler"></a>**CheckForHangHandler**  
[*MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)は不要な中間のドライバーのためこのエントリ ポイントを設定する必要があります**NULL**します。

<a href="" id="resethandlerex"></a>**ResetHandlerEx**  
[*MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)は不要な中間のドライバーのためこのエントリ ポイントを設定する必要があります**NULL**します。

<a href="" id="devicepnpeventnotifyhandler"></a>**DevicePnPEventNotifyHandler**  
エントリ ポイント、 [ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)関数。

<a href="" id="shutdownhandlerex"></a>**ShutdownHandlerEx**  
[*MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)は必要な関数です。 *MiniportShutdownEx*仮想ミニポートを初期状態に戻します (中間のドライバーの前に**DriverEntry**ルーチンの実行)。

<a href="" id="canceloidrequesthandler"></a>**CancelOidRequestHandler**  
[*MiniportCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request)は必要な関数です。 NDIS 呼び出し*MiniportCancelOidRequest* OID 要求を取り消します。

中間のドライバーには、その他の必要があります*MiniportXxx*実装に固有である関数。 省略可能な登録方法の詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

特定ミニポート ドライバー ハンドラー関数は、中間のドライバーによって提供されることはありません。 理由が考えられます。 このようなドライバーは、割り込みのデバイスを管理しないか、このようなドライバーが発生した IRQL でバッファーを割り当てられません。

**注**  中間ドライバーが一時停止を含めるし、機能を再起動する必要があります。 一時停止のサポートが含まれてし、NDIS は、基になるドライバー スタックを置いたときに必要な場合は、仮想のミニポートの再起動します。 一時停止と再起動の詳細については、次を参照してください。[ドライバー スタック管理](driver-stack-management.md)します。

 

 

 





