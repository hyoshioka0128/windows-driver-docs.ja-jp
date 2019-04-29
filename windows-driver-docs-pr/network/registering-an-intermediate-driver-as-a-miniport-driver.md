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
ms.openlocfilehash: 36c74262f88f6b25b759053172339e1891f73b57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391966"
---
# <a name="registering-an-intermediate-driver-as-a-miniport-driver"></a>中間ドライバーのミニポート ドライバーとしての登録





中間のドライバーは呼び出し[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)をエクスポートするその*MiniportXxx*関数。 *NdisMiniportDriverHandle*によって返される**NdisMRegisterMiniportDriver**中間ドライバーによって保持および NDIS ドライバーを呼び出すときに入力する必要があります[ **NdisIMInitializeDeviceInstanceEx**](https://msdn.microsoft.com/library/windows/hardware/ff562727)します。

中間のドライバーが必要です。

1.  0 に初期化する[ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造体[ **NdisZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff564698).

2.  必須の住所は格納*MiniportXxx*関数、省略可能なあらゆるとして*MiniportXxx*ドライバーをエクスポートする関数。

NDIS 6.0 の機能をサポートする中間のドライバーは、バージョン 6.0 のミニポート ドライバーとして登録する必要があります。 ミニポート ドライバーのバージョン番号を指定する方法については、次を参照してください。 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)します。

次のエントリを設定する必要があります*MiniportCharacteristics*を有効な*MiniportXxx*関数のアドレスでない場合、関数オプションはエクスポートされません。 ドライバーが、関数をエクスポートされない場合は、アドレスを設定**NULL**します。

<a href="" id="setoptionshandler"></a>**SetOptionsHandler**  
[*MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数は省略可能です。 NDIS 呼び出し*MiniportSetOptions*のため中間ドライバーは、省略可能なハンドラーを指定できるようにします。

<a href="" id="initializehandlerex"></a>**InitializeHandlerEx**  
NDIS 呼び出し[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)中間ドライバー呼び出しの結果**NdisIMInitializeDeviceInstanceEx**はミニポート アダプターを初期化するには初期化されている仮想ミニポートの操作。

<a href="" id="halthandlerex"></a>**HaltHandlerEx**  
[*MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)は必要な関数です。 NDIS 呼び出し*MiniportHaltEx*中間ドライバーが公開されているミニポート仮想デバイスが無効または停止している場合、または中間のドライバーが呼び出された場合[ **NdisIMDeInitializeDeviceInstance**](https://msdn.microsoft.com/library/windows/hardware/ff562721)その削除を開始します。

<a href="" id="unloadhandler"></a>**UnloadHandler**  
[*MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)は必要な関数です。 NDIS 呼び出し*MiniportDriverUnload*中間ドライバーをアンロードします。

<a href="" id="pausehandler"></a>**PauseHandler**  
[*MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)は必要な関数です。 NDIS 呼び出し*MiniportPause*中間ドライバーの場合は、指定した仮想ミニポート経由のネットワーク データの流れを停止します。

<a href="" id="restarthandler"></a>**RestartHandler**  
[**MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)は必要な関数です。 NDIS 呼び出し*MiniportRestart*中間ドライバーの場合は、指定した仮想ミニポートを通してネットワーク データのフローが再起動します。

<a href="" id="oidrequesthandler"></a>**OidRequestHandler**  
[*MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416) OID を受け取る\_*XXX*と呼ばれる上位のドライバーから送信された要求[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)または NDIS から。 中間のドライバーは、要求を処理または、基になるミニポート ドライバーに渡す可能性があります。

<a href="" id="sendnetbufferlistshandler"></a>**SendNetBufferListsHandler**  
[*MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)を 1 つまたは複数のポインターの配列を受け取る[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ネットワークを指定する構造体ネットワーク経由で伝送されるデータ。 すべての中間ドライバーを指定する必要があります、 *MiniportSendNetBufferLists*関数。 詳細については、次を参照してください。[送信ネットワーク データを、中間ドライバー](transmitting-network-data-through-an-intermediate-driver.md)します。

<a href="" id="returnnetbufferlistshandler"></a>**ReturnNetBufferListsHandler**  
[*MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)返された受信[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体に示されていましたが、呼び出すことによってより高度なドライバー **NdisMIndicateReceiveNetBufferLists**します。 呼び出し**NdisMIndicateReceiveNetBufferLists**上位レベルのドライバーに示されるリソースの制御を解放します。 中間のドライバーが NET に割り当てられた後、各を示す値より高度なドライバーが消費する\_バッファー\_をリストの構造とについて説明しますが、リソースが返されます、 *MiniportReturnNetBufferLists*関数。

<a href="" id="cancelsendhandler"></a>**CancelSendHandler**  
[*MiniportCancelSend* ](https://msdn.microsoft.com/library/windows/hardware/ff559342)は必要な関数です。 NDIS 呼び出し*MiniportCancelSend*送信要求を取り消します。

<a href="" id="checkforhanghandler"></a>**CheckForHangHandler**  
[*MiniportCheckForHangEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559346)は不要な中間のドライバーのためこのエントリ ポイントを設定する必要があります**NULL**します。

<a href="" id="resethandlerex"></a>**ResetHandlerEx**  
[*MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)は不要な中間のドライバーのためこのエントリ ポイントを設定する必要があります**NULL**します。

<a href="" id="devicepnpeventnotifyhandler"></a>**DevicePnPEventNotifyHandler**  
エントリ ポイント、 [ *MiniportDevicePnPEventNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff559369)関数。

<a href="" id="shutdownhandlerex"></a>**ShutdownHandlerEx**  
[*MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)は必要な関数です。 *MiniportShutdownEx*仮想ミニポートを初期状態に戻します (中間のドライバーの前に**DriverEntry**ルーチンの実行)。

<a href="" id="canceloidrequesthandler"></a>**CancelOidRequestHandler**  
[*MiniportCancelOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559339)は必要な関数です。 NDIS 呼び出し*MiniportCancelOidRequest* OID 要求を取り消します。

中間のドライバーには、その他の必要があります*MiniportXxx*実装に固有である関数。 省略可能な登録方法の詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

特定ミニポート ドライバー ハンドラー関数は、中間のドライバーによって提供されることはありません。 理由が考えられます。 このようなドライバーは、割り込みのデバイスを管理しないか、このようなドライバーが発生した IRQL でバッファーを割り当てられません。

**注**  中間ドライバーが一時停止を含めるし、機能を再起動する必要があります。 一時停止のサポートが含まれてし、NDIS は、基になるドライバー スタックを置いたときに必要な場合は、仮想のミニポートの再起動します。 一時停止と再起動の詳細については、次を参照してください。[ドライバー スタック管理](driver-stack-management.md)します。

 

 

 





