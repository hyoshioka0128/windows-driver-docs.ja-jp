---
title: EFI_USBFN_IO_PROTOCOL.Transfer
description: EFI_USBFN_IO_PROTOCOL.Transfer
ms.assetid: 0585de75-9268-4964-8c5f-dcc3338e5287
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f45877b8a785f11f09f6672e3a349e4489b323
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337674"
---
# <a name="efiusbfnioprotocoltransfer"></a>EFI\_USBFN\_IO\_プロトコル。転送


**転送**関数の指定したエンドポイントのホスト間でデータを転送するハンドル。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Direction</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiUsbEndpointDirectionDeviceTx</p></td>
<td><p>指定のエンドポイントで送信転送を開始し、すぐに返します。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbEndpointDirectionDeviceRx</p></td>
<td><p>指定されたエンドポイントで受信転送を開始し、使用可能なデータをすぐに返します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI *EFI_USBFN_IO_TRANSFER) (
  IN EFI_USBFN_IO_PROTOCOL         *This,
  IN UINT8                         EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION  Direction,
  IN OUT UINTN                     *BufferSize,
  IN OUT VOID                      *Buffer
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="endpointindex"></a>*EndpointIndex*  
転送を行う必要が送信と受信のエンドポイントを示します。

<a href="" id="direction"></a>*方向*  
エンドポイントの方向です。 詳細については、次を参照してください。 [EFI\_USBFN\_エンドポイント\_方向](efi-usbfn-endpoint-direction.md)します。

<a href="" id="buffersize"></a>*BufferSize*  
方向が場合**EfiUsbEndpointDirectionDeviceRx**:入力バッファーのバイト単位のサイズ。 出力では、データの量は、バッファーのバイト単位で返されます。 方向が場合**EfiUsbEndpointDirectionDeviceTx**:入力バッファーのバイト単位のサイズ。 出力で、実際に転送されるデータ量 (バイト単位)。

<a href="" id="buffer"></a>*バッファー*  
方向が場合**EfiUsbEndpointDirectionDeviceRx**: バッファーを受信したデータを返します。

方向が場合**EfiUsbEndpointDirectionDeviceTx**:転送するデータを格納するバッファー。

**注**  このバッファーが割り当てられ、AllocateTransferBuffer と FreeTransferBuffer 関数を使用して解放します。 この関数の呼び出し元は、無料またはまでバッファーを再利用する必要がありますいないを**EfiUsbMsgEndpointStatusChangedRx**または**EfiUsbMsgEndpointStatusChangedTx**のアドレスと共にメッセージを受信した、メッセージ ペイロードの一部としてバッファーに転送します。 参照してください[EFI\_USBFN\_IO\_プロトコル。EventHandler](efi-usbfn-io-protocoleventhandler.md)さまざまなメッセージとそのペイロードの詳細についてはします。

 

## <a name="return-values"></a>戻り値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EFI_SUCCESS</strong></p></td>
<td><p>正常に返される関数</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>パラメーターが無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理デバイスがビジー状態か、この要求を処理する準備ができていません</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


クラスのドライバーを呼び出す必要があります[EFI\_USBFN\_IO\_プロトコル。EventHandler](efi-usbfn-io-protocoleventhandler.md)転送の状態と、さまざまなエンドポイントに転送されたバイト数の更新プログラムを受信するには、繰り返し。 転送の状態、更新時に、*バッファー*のフィールド、 [EFI\_USBFN\_転送\_結果](efi-usbfn-transfer-result.md)がバッファーのポインターでは、構造体を初期化する必要がありますこのメソッドに渡されます。 この関数は、efi を搭載したが失敗した\_無効な\_パラメーターが指定した方向がエンドポイントの正しくない場合、コードを返します。

呼び出しシーケンスの概要を示した[UEFI シーケンス図](uefi-sequence-diagram.md)します。

この関数は、efi を搭載したが失敗した\_無効な\_パラメーターが指定した方向がエンドポイントの正しくない場合、コードを返します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




