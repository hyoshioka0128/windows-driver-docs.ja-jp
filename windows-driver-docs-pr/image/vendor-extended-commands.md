---
title: ベンダー拡張コマンド
description: ベンダー拡張コマンド
ms.assetid: 3d360a9f-5a65-452b-a8ad-080dc7d8c8f5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a53ae7a1f478a068540fe8cbf4a1d46086e5e9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840724"
---
# <a name="vendor-extended-commands"></a>ベンダー拡張コマンド





アプリケーションは、 **Iwiaitemextras:: Escape**メソッドを使用してデバイスに任意のコマンドを送信できます。これについては、Microsoft Windows SDK のドキュメントを参照してください。 ルート項目に対して**QueryInterface**を呼び出すことによって、 **Iwiaitemextras**インターフェイスへのポインターを取得できます。 その後、アプリケーションは、任意のオペコードとパラメーターを使用して PTP コマンドを構築し、このコマンドをデバイスに送信できます。 また、アプリケーションは、デバイスとの間でデータを送受信することもできます。

デバイスは、 **Iwiaitemextras:: Escape**メソッドから制御が戻ったときに、操作の結果をアプリケーションに通知します。これにより、 [**PTP\_ベンダ\_DATA\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_out)構造体に応答コードと応答パラメーターが入力されます。 構造に含まれている[**PTP\_ベンダ\_データ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_in)の**SessionId**メンバーと**transactionid**メンバーは無視されます。 ドライバーは、これらの値に適切な値を提供します。

エスケープ\_以外のベンダー定義コマンドについては、\_停止を明確に\_します。また、特殊なフラグ、エスケープ\_PTP\_VENDOR\_コマンドを、 **Iwiaitemextras:: ESCAPE**メソッドで使用されるコマンドと組み合わせて使用する必要があります (または演算子を使用します)。 ベンダー定義のコマンドが、次に示すフラグを使用してデバイス上のオブジェクトを作成または削除する場合、ドライバーはその内部構造からオブジェクトを追加または削除し、WIA イベントを生成します。 その他のすべての標準コマンドは、適切な WIA インターフェイスを使用して発行する必要があります。

**Iwiaitemextras:: Escape**の最初のパラメーターは、次のフラグの1つ以上を組み合わせたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エスケープコード</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_CMD</p></td>
<td><p>オブジェクトが追加され、オブジェクトのハンドルがいずれかのコマンドパラメーターに含まれています。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_CMD</p></td>
<td><p>オブジェクトを削除しようとしています。オブジェクトのハンドルは、いずれかのコマンドパラメーターに含まれています。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_RESP</p></td>
<td><p>オブジェクトが追加され、オブジェクトのハンドルが応答パラメーターの1つに含まれています。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_RESP</p></td>
<td><p>オブジェクトを削除しています。また、オブジェクトのハンドルが応答パラメーターの1つに含まれています。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM1</p></td>
<td><p>追加または削除されたオブジェクトのハンドルは、コマンドまたは応答の最初のパラメーターに含まれています。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM2</p></td>
<td><p>追加または削除されたオブジェクトのハンドルは、コマンドまたは応答の2番目のパラメーターにあります。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM3</p></td>
<td><p>追加または削除されたオブジェクトのハンドルは、コマンドまたは応答の3番目のパラメーターにあります。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM4</p></td>
<td><p>追加または削除されたオブジェクトのハンドルは、コマンドまたは応答の4番目のパラメーターにあります。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM5</p></td>
<td><p>追加または削除されたオブジェクトのハンドルは、コマンドまたは応答の5番目のパラメーターにあります。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_CLEAR_STALLS</p></td>
<td><p>ベンダ拡張コマンドによって発生するエラー状態をすべてクリアします。 このフラグは、他のフラグと組み合わせて使用することはできません。 このフラグの詳細については、この表の後の注を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_VENDOR_COMMAND</p></td>
<td><p>コマンドは、ベンダーによって拡張されたコマンドです。</p></td>
</tr>
</tbody>
</table>

 

アプリケーションが**Iwiaitemextras:: escape**をエスケープ\_\_使用して、このメソッドの最初の引数として\_ストールフラグをクリアする**場合  、** ドライバーは ptp **Get Device Status**要求を発行して、いずれかのエンドポイントが停止状態にあるかどうかを判断します。 "**デバイスの状態の取得**" コマンドが成功した場合、ドライバーは、そのようなエンドポイントごとにパイプの USB 制御コード[ **\_\_リセットする IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_reset_pipe)を発行します。 **Get Device Status**コマンドが失敗した場合、ドライバーは PTP**デバイスリセット**要求を発行します。 **デバイスの状態の取得**と**デバイスのリセット**については、Usb 静止イメージキャプチャデバイスの定義 (USB SICDD) のピマ 15740:2000 standard、First Edition、および Revision 1.0 を参照してください。

 

次のサンプルコードは、ベンダ拡張コマンドインターフェイスの使用方法を示しています。 コードに*ptpusd .h*ヘッダーが含まれていることを確認してください。これには、エスケープコードとその他の定数の定義が含まれています。また、 [**ptp\_ベンダ\_データ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_in) 、および[**ptp\_ベンダー\_データ\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_out)構造を格納していることを確認してください。 **Iwiaitemextras**インターフェイスは、ルート項目で**QueryInterface**を呼び出すことによって取得されます。 このルート項目へのポインターである*Piwiarootitem*は、たとえば、 **Iwiadevmgr:: SelectDeviceDlg**を呼び出すことによって取得できます (詳細については、Microsoft Windows SDK のドキュメントを参照してください)。

```cpp
//
// Test IWiaItemExtras::Escape method
//
HRESULT hr = S_OK;
IWiaItemExtras *pIWiaItemExtras = NULL;

hr = pIWiaRootItem->QueryInterface(IID_IWiaItemExtras,
                                   (VOID **) &pIWiaItemExtras);
if (FAILED(hr)) {
    MessageBox("QueryInterface for IWiaItemExtras failed");
    return;
}

PTP_VENDOR_DATA_IN *pDataIn = NULL;
PTP_VENDOR_DATA_OUT *pDataOut = NULL;
DWORD dwDataInSize = SIZEOF_REQUIRED_VENDOR_DATA_IN;
DWORD dwDataOutSize = SIZEOF_REQUIRED_VENDOR_DATA_OUT + 0x1000;
DWORD dwActualDataOutSize = 0;

pDataIn = (PTP_VENDOR_DATA_IN *) CoTaskMemAlloc(dwDataInSize);
if (!pDataIn) {
    MessageBox("CoTaskMemAlloc failed");
    return;
}

pDataOut = (PTP_VENDOR_DATA_OUT *) CoTaskMemAlloc(dwDataOutSize);
if (!pDataOut) {
 CoTaskMemFree(pDataIn);
    MessageBox("CoTaskMemAlloc failed");
    return;
}
ZeroMemory(pDataIn, dwDataInSize);
ZeroMemory(pDataOut, dwDataOutSize);

pDataIn->OpCode = 0x1001;
pDataIn->SessionId = 0;     // The driver will fill this in.
pDataIn->TransactionId = 0; // The driver will fill this in.
pDataIn->NumParams = 0;

//
// pDataIn->NextPhase informs the PTP driver whether to 
// read data from the device (as shown), or
// write data to the device (use PTP_NEXTPHASE_WRITE_DATA),
// to neither read nor write data (use PTP_NEXTPHASE_NO_DATA).
//
pDataIn->NextPhase = PTP_NEXTPHASE_READ_DATA;

hr = pIWiaItemExtras->Escape(ESCAPE_PTP_VENDOR_COMMAND,
                             (BYTE *) pDataIn, dwDataInSize,
                             (BYTE *) pDataOut, dwDataOutSize,
                             &dwActualDataOutSize);

if (FAILED(hr)) {
    MessageBox("Escape failed");
    return;
}

//
// Data returned from device is located at pDataOut->VendorReadData.
//
```

 

 




