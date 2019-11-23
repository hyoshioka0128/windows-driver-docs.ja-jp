---
title: 中間ドライバーのミニポート ドライバーとしての登録
description: 中間ドライバーのミニポート ドライバーとしての登録
ms.assetid: a01bc0f4-4a03-4d44-88c0-7029042d6953
keywords:
- 中間ドライバーの登録
- 中間ドライバー WDK ネットワーク、登録
- NDIS 中間ドライバー WDK、登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bcd14daa235809e21b47446e4279c68b8a23708
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842108"
---
# <a name="registering-an-intermediate-driver-as-a-miniport-driver"></a>中間ドライバーのミニポート ドライバーとしての登録





中間ドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出して、その*miniportxxx*関数をエクスポートします。 **NdisMRegisterMiniportDriver**によって返される*NdisMiniportDriverHandle*は、ドライバーが[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)を呼び出すときに、中間ドライバーによって保持され、NDIS に入力する必要があります。

中間ドライバーには次のものが必要です。

1.  [**NdisZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiszeromemory)を使用して、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造をゼロ初期化します。

2.  必須の*Miniportxxx*関数のアドレスと、ドライバーによってエクスポートされるオプションの*miniportxxx*関数を格納します。

NDIS 6.0 の機能をサポートする中間ドライバーは、バージョン6.0 のミニポートドライバーとして登録する必要があります。 ミニポートドライバーのバージョン番号を指定する方法の詳細については、「 [**NDIS\_ミニポート\_ドライバー\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)」を参照してください。

関数が省略可能であり、エクスポートされていない場合は、 *Miniportcharacteristics*の次のエントリを有効な*miniportcharacteristics*関数のアドレスに設定する必要があります。 ドライバーが関数をエクスポートしない場合は、アドレスを**NULL**に設定します。

<a href="" id="setoptionshandler"></a>**SetOptionsHandler**  
[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)は省略可能な関数です。 NDIS は*MiniportSetOptions*を呼び出して、中間ドライバーがオプションのハンドラーを指定できるようにします。

<a href="" id="initializehandlerex"></a>**Initializeハンドラ Ex**  
NDIS は、初期化中の仮想ミニポートに対して、NdisIMInitializeDeviceInstanceEx を呼び出して、そのミニポートアダプター操作を初期化するために、中間ドライバーがを呼び出した結果として[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出します。

<a href="" id="halthandlerex"></a>**HaltHandlerEx**  
[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)は必須の機能です。 中間ドライバーが公開されている仮想ミニポートデバイスが無効になっているか停止している場合、または中間ドライバーが[**NdisIMDeInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance)を呼び出して削除を開始した場合、NDIS は*Miniporthaltex*を呼び出します。

<a href="" id="unloadhandler"></a>**UnloadHandler**  
[*Miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)は必須の機能です。 NDIS は、 *Miniportdriverunload*を呼び出して中間ドライバーをアンロードします。

<a href="" id="pausehandler"></a>**PauseHandler**  
[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)は必須の機能です。 NDIS は、 *Miniportpause*を呼び出して、中間ドライバーの指定した仮想ミニポートを介してネットワークデータのフローを停止します。

<a href="" id="restarthandler"></a>**RestartHandler**  
[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)は必須の機能です。 NDIS は、 *Miniportrestart*を呼び出して、中間ドライバーの指定した仮想ミニポートを介してネットワークデータのフローを再開します。

<a href="" id="oidrequesthandler"></a>**OidRequestHandler**  
[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)は、 [**NDISOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)または NDIS から呼び出された、それ以降のドライバーから送信された、OID\_*XXX*の要求を受け取ります。 中間ドライバーは、要求を処理するか、基になるミニポートドライバーに渡すことができます。

<a href="" id="sendnetbufferlistshandler"></a>**SendNetBufferListsHandler**  
[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)は、ネットワーク経由で送信するネットワークデータを指定する[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体への1つ以上のポインターの配列を受け取ります。 すべての中間ドライバーは、 *Miniportsendnetbufferlists*関数を提供する必要があります。 詳細については、「[中間ドライバーを使用したネットワークデータの転送](transmitting-network-data-through-an-intermediate-driver.md)」を参照してください。

<a href="" id="returnnetbufferlistshandler"></a>**ReturnNetBufferListsHandler**  
[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)は、 **NdisMIndicateReceiveNetBufferLists**を呼び出すことによって上位レベルのドライバーに対して以前に指定した、返された[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を受け取ります。 **NdisMIndicateReceiveNetBufferLists**を呼び出すと、上位レベルのドライバーに示されているリソースの制御が解放されます。 上位レベルのドライバーが各表示を使用した後、中間ドライバーによって割り当てられた NET\_BUFFER\_LIST 構造体と、その中に記述されているリソースが、 *Miniportreturnnetbufferlists*関数に返されます。

<a href="" id="cancelsendhandler"></a>**CancelSendHandler**  
[*Miniportcancelsend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send)は必須の機能です。 NDIS は*Miniportcancelsend*を呼び出して、送信要求を取り消します。

<a href="" id="checkforhanghandler"></a>**CheckForHangHandler**  
[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)は中間ドライバーには必要ないため、このエントリポイントを**NULL**に設定する必要があります。

<a href="" id="resethandlerex"></a>**ResetHandlerEx**  
[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)は、中間ドライバーには必要ありません。そのため、このエントリポイントを**NULL**に設定する必要があります。

<a href="" id="devicepnpeventnotifyhandler"></a>**DevicePnPEventNotifyHandler**  
[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数のエントリポイント。

<a href="" id="shutdownhandlerex"></a>**Shutdownハンドラ Ex**  
[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)は必須の関数です。 *Miniportshutdownex*は、仮想ミニポートを初期状態に復元します (中間ドライバーの**driverentry**ルーチンが実行される前)。

<a href="" id="canceloidrequesthandler"></a>**CancelOidRequestHandler**  
[*Miniportcanceloidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)は必須の機能です。 NDIS は、この OID 要求を取り消すために*Miniportcanceloidrequest*を呼び出します。

中間ドライバーでは、実装固有の他の*Miniportxxx*関数が必要になる場合があります。 オプションの登録の詳細については、「[オプションのミニポートドライバーサービスの構成](configuring-optional-miniport-driver-services.md)」を参照してください。

特定のミニポートドライバーハンドラー関数は、中間ドライバーによって提供されることはありません。 その理由は、このようなドライバーでは、中断しているデバイスを管理しないこと、または、発生した IRQL でバッファーが割り当てられない場合などです。

**注**  中間ドライバーには、一時停止と再起動の機能が含まれている必要があります。 NDIS が基になるドライバースタックを一時停止するときに、必要に応じて、仮想ミニポートの一時停止と再起動のサポートを含めます。 一時停止と再起動の詳細については、「[ドライバースタック管理](driver-stack-management.md)」を参照してください。

 

 

 





