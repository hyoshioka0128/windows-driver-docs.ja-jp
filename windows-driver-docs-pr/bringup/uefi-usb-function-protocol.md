---
title: UEFI USB 関数プロトコル
description: UEFI USB 関数プロトコル
ms.assetid: eac35cf4-82b4-4d7e-ae69-8f506f12ae5d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06f53d5ab7c43b9b1f7212f7cbb3df233d23c300
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337364"
---
# <a name="uefi-usb-function-protocol"></a>UEFI USB 関数プロトコル


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサ アーキテクチャにのみ適用可能性があります。

 

USB 関数のプロトコルでは、UEFI 環境でジェネリックかつ軽量な USB トランスポートを定義します。 このプロトコルは、点滅ツール、USB 大容量記憶装置のモード、および UEFI 環境が起動したデバイスとホスト コンピューター間の双方向通信を必要とするその他のツールによって使用されます。

## <a name="efiusbfnioprotocol"></a>EFI\_USBFN\_IO\_プロトコル


USB のエントリ ポイント関数のドライバーの接続を他の UEFI デバイス ドライバーなど**EFI\_ドライバー\_バインド\_プロトコル**のイメージのハンドルを**EFI\_USBFN\_IO\_プロトコル**ドライバー

ドライバーのバインディング プロトコルには、3 つのサービスが含まれています。**サポートされている**、**開始**、および**停止**します。 **サポートされている**関数がこのドライバーが特定のコント ローラーをサポートしているかどうかをテストする必要があります。 **開始**関数する必要がありますが必要な場合は、USB コント ローラーに電力を供給、ハードウェアと内部データ構造体を初期化およびを返します。 ポートは、この関数によってアクティブ化されませんする必要があります。 **停止**関数は、必要な場合は、実行/ストップ ビットおよび電源オフの USB コント ローラーをリセットすることで、デバイスを無効にする必要があります。

**GUID**

```cpp
// {32D2963A-FE5D-4f30-B633-6E5DC55803CC}
#define EFI_USBFN_IO_PROTOCOL_GUID \
  {0x32d2963a, 0xfe5d, 0x4f30, 0xb6, 0x33, 0x6e, 0x5d, 0xc5, \
   0x58, 0x3, 0xcc };
```

**リビジョン番号**

```cpp
#define EFI_USBFN_IO_PROTOCOL_REVISION   0x00010002
```

**プロトコル インターフェイス構造体**

```cpp
typedef struct _EFI_USBFN_IO_PROTOCOL 
{
  UINT32                                      Revision;
  EFI_USBFN_IO_DETECT_PORT                    DetectPort;
  EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS     ConfigureEnableEndpoints;
  EFI_USBFN_IO_GET_ENDPOINT_MAXPACKET_SIZE    GetEndpointMaxPacketSize;
  EFI_USBFN_IO_GET_DEVICE_INFO                GetDeviceInfo;
  EFI_USBFN_IO_GET_VENDOR_ID_PRODUCT_ID       GetVendorIdProductId;
  EFI_USBFN_IO_ABORT_TRANSFER                 AbortTransfer;
  EFI_USBFN_IO_GET_ENDPOINT_STALL_STATE       GetEndpointStallState; 
  EFI_USBFN_IO_SET_ENDPOINT_STALL_STATE       SetEndpointStallState;
  EFI_USBFN_IO_EVENTHANDLER                   EventHandler;
  EFI_USBFN_IO_TRANSFER                       Transfer;
  EFI_USBFN_IO_GET_MAXTRANSFER_SIZE           GetMaxTransferSize;
  EFI_USBFN_IO_ALLOCATE_TRANSFER_BUFFER       AllocateTransferBuffer;
  EFI_USBFN_IO_FREE_TRANSFER_BUFFER           FreeTransferBuffer;
  EFI_USBFN_IO_START_CONTROLLER               StartController;
  EFI_USBFN_IO_STOP_CONTROLLER                StopController;
  EFI_USBFN_IO_SET_ENDPOINT_POLICY            SetEndpointPolicy;
  EFI_USBFN_IO_GET_ENDPOINT_POLICY            GetEndpointPolicy;
  EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS_EX  ConfigureEnableEndpointsEx;
} EFI_USBFN_IO_PROTOCOL;
```

### <a name="members"></a>メンバー

<a href="" id="revision"></a>**リビジョン**  
リビジョン、 **EFI\_USBFN\_IO\_プロトコル**準拠します。 すべての将来のリビジョンは、旧バージョンと互換性のあるである必要があります。 場合は、今後のバージョンは旧バージョンと互換性のある、別の GUID を使用する必要があります。

<a href="" id="detectport"></a>**DetectPort**  
USB ポートの種類に関する情報を返します。 参照してください[EFI\_USBFN\_IO\_プロトコル。DetectPort](efi-usbfn-io-protocoldetectport.md)します。

<a href="" id="configureenableendpoints"></a>**ConfigureEnableEndpoints**  
指定されたデバイスと構成記述子に基づいてすべてのエンドポイントを初期化します。 実行/ストップ ビットを設定して、デバイスを有効にします。 参照してください[EFI\_USBFN\_IO\_プロトコル。ConfigureEnableEndpoints](efi-usbfn-io-protocolconfigureenableendpoints.md)します。

<a href="" id="getendpointmaxpacketsize"></a>**GetEndpointMaxPacketSize**  
指定したエンドポイントの最大パケット サイズを返します。 参照してください[EFI\_USBFN\_IO\_プロトコル。GetEndpointMaxPacketSize](efi-usbfn-io-protocolgetendpointmaxpacketsize.md)します。

<a href="" id="getdeviceinfo"></a>**GetDeviceInfo**  
Unicode 文字列として提供された識別子に基づくデバイス固有の情報を返します。 参照してください[EFI\_USBFN\_IO\_プロトコル。GetDeviceInfo](efi-usbfn-io-protocolgetdeviceinfo.md)します。

<a href="" id="getvendoridproductid"></a>**GetVendorIdProductId**  
ベンダー id とデバイスの製品 id を返します。 参照してください[EFI\_USBFN\_IO\_プロトコル。GetVendorIdProductId](efi-usbfn-io-protocolgetvendoridproductid.md)します。

<a href="" id="aborttransfer"></a>**AbortTransfer**  
指定のエンドポイントでの転送を中止します。 参照してください[EFI\_USBFN\_IO\_プロトコル。AbortTransfer](efi-usbfn-io-protocolaborttransfer.md)します。

<a href="" id="getendpointstallstate"></a>**GetEndpointStallState**  
指定したエンドポイントの停止の状態を返します。 参照してください[EFI\_USBFN\_IO\_プロトコル。GetEndpointStallState](efi-usbfn-io-protocolgetendpointstallstate.md)します。

<a href="" id="setendpointstalls"></a>**SetEndpointStallS**  
設定または指定したエンドポイントの停止状態をクリアします。 参照してください[EFI\_USBFN\_IO\_プロトコル。SetEndpointStallState](efi-usbfn-io-protocolsetendpointstallstate.md)します。

<a href="" id="eventhandler"></a>**EventHandler**  
この関数は、USB バス状態の更新プログラムを受信、受信、エンドポイントの完全なイベントと 0 のエンドポイントでセットアップ パケットを送信する繰り返し呼び出されます。 参照してください[EFI\_USBFN\_IO\_プロトコル。EventHandler](efi-usbfn-io-protocoleventhandler.md)します。

<a href="" id="transfer"></a>**転送**  
この関数は、指定した方向に応じて、指定されたエンドポイントで、ホスト間でデータの転送を処理します。 参照してください[EFI\_USBFN\_IO\_プロトコル。転送](efi-usbfn-io-protocoltransfer.md)します。

<a href="" id="getmaxtransfersize"></a>**GetMaxTransferSize**  
バイト単位でサポートされている転送の最大サイズ。 参照してください[EFI\_USBFN\_IO\_プロトコル。GetMaxTransferSize](efi-usbfn-io-protocolgetmaxtransfersize.md)します。

<a href="" id="allocatetransferbuffer"></a>**AllocateTransferBuffer**  
転送をコント ローラーの要件を満たす、指定されたサイズのバッファーを割り当てます。 参照してください[EFI\_USBFN\_IO\_プロトコル。AllocateTransferBuffer](efi-usbfn-io-protocolallocatetransferbuffer.md)します。

<a href="" id="freetransferbuffer"></a>**FreeTransferBuffer**  
転送バッファーごとに割り当てられたメモリの割り当てを解除、 **AllocateTransferBuffer**関数。 参照してください[EFI\_USBFN\_IO\_プロトコル。FreeTransferBuffer](efi-usbfn-io-protocolfreetransferbuffer.md)します。

<a href="" id="startcontroller"></a>**StartController**  
必要な場合は、USB コント ローラーに電力を供給し、ハードウェアおよび内部データ構造体を初期化します。 参照してください[EFI\_USBFN\_IO\_プロトコル。StartController](efi-usbfn-io-protocolstartcontroller.md)します。 この関数は、以降、プロトコルのリビジョン 0x00010001 で使用できます。

<a href="" id="stopcontroller"></a>**StopController**  
必要な場合は、実行/ストップ ビットと電源オフ、USB コント ローラーをリセットすることで、デバイスを無効にします。 参照してください[EFI\_USBFN\_IO\_プロトコル。StopController](efi-usbfn-io-protocolstopcontroller.md)します。 この関数は、以降、プロトコルのリビジョン 0x00010001 で使用できます。

<a href="" id="setendpointpolicy"></a>**SetEndpointPolicy**  
指定したコントロール以外のエンドポイントの構成ポリシーを設定します。 参照してください[EFI\_USBFN\_IO\_プロトコル。SetEndpointPolicy](efi-usbfn-io-protocolsetendpointpolicy.md)します。 この関数は、以降、プロトコルのリビジョン 0x00010001 で使用できます。

<a href="" id="getendpointpolicy"></a>**GetEndpointPolicy**  
指定したコントロール以外のエンドポイントの構成ポリシーを取得します。 参照してください[EFI\_USBFN\_IO\_プロトコル。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)します。 この関数は、以降、プロトコルのリビジョン 0x00010001 で使用できます。

<a href="" id="configureenableendpointsex"></a>**ConfigureEnableEndpointsEx**  
デバイスと構成記述子で最高の速度 (SuperSpeed) までのハードウェアでサポートを選択して、すべてのエンドポイントを初期化します。 デバイスを有効するには、実行/ストップ ビットを設定します。 参照してください[EFI\_USBFN\_IO\_プロトコル。ConfigureEnableEndpointsEx](efi-usbfn-io-protocol-configureenableendpointsex.md)します。 この関数は、以降、プロトコルのリビジョン 0x00010002 で使用できます。

### <a name="remarks"></a>注釈

次の表の各バージョンでサポートされている関数、 **EFI\_USBFN\_IO\_プロトコル**プロトコル。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>リビジョン 0x00010002</th>
<th>リビジョン 0x00010001</th>
<th>リビジョン 0x00010000</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConfigureEnableEndpointsEx</strong></p></td>
<td><p><strong>DetectPort</strong></p>
<p><strong>ConfigureEnableEndpoints</strong></p>
<p><strong>GetEndpointMaxPacketSize</strong></p>
<p><strong>GetDeviceInfo</strong></p>
<p><strong>GetVendorIdProductId</strong></p>
<p><strong>AbortTransfer</strong></p>
<p><strong>GetEndpointStallState</strong></p>
<p><strong>SetEndpointStallState</strong></p>
<p><strong>EventHandler</strong></p>
<p><strong>転送</strong></p>
<p><strong>GetMaxTransferSize</strong></p>
<p><strong>AllocateTransferBuffer</strong></p>
<p><strong>FreeTransferBuffer</strong></p>
<p><strong>StartController</strong></p>
<p><strong>StopController</strong></p>
<p><strong>SetEndpointPolicy</strong></p>
<p><strong>GetEndpointPolicy</strong></p></td>
<td><p><strong>DetectPort</strong></p>
<p><strong>ConfigureEnableEndpoints</strong></p>
<p><strong>GetEndpointMaxPacketSize</strong></p>
<p><strong>GetDeviceInfo</strong></p>
<p><strong>GetVendorIdProductId</strong></p>
<p><strong>AbortTransfer</strong></p>
<p><strong>GetEndpointStallState</strong></p>
<p><strong>SetEndpointStallState</strong></p>
<p><strong>EventHandler</strong></p>
<p><strong>転送</strong></p>
<p><strong>GetMaxTransferSize</strong></p>
<p><strong>AllocateTransferBuffer</strong></p>
<p><strong>FreeTransferBuffer</strong></p></td>
</tr>
</tbody>
</table>
