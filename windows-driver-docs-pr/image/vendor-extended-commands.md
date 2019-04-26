---
title: ベンダー拡張コマンド
description: ベンダー拡張コマンド
ms.assetid: 3d360a9f-5a65-452b-a8ad-080dc7d8c8f5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ea83d3dc71207a59612ca4ab3a307bbabc0f9ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356128"
---
# <a name="vendor-extended-commands"></a>ベンダー拡張コマンド





アプリケーションを使用してデバイスに任意のコマンドを送信することができます、 **IWiaItemExtras::Escape**メソッドは、Microsoft Windows SDK ドキュメントで説明します。 呼び出して**QueryInterface**ルート アイテムへのポインターを取得することができます、 **IWiaItemExtras**インターフェイス。 アプリケーションは任意のオペコードとパラメーターを使用して PTP コマンドを作成し、デバイスにこのコマンドを送信します。 アプリケーションもデータを送信したり、デバイスからデータを受信できます。

デバイス操作の結果をアプリケーションに通知時に、 **IWiaItemExtras::Escape**メソッドから返される応答コードと応答のパラメーターに入力し、 [ **PTP\_仕入先\_データ\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff546452)構造体。 **SessionId**と**TransactionId**のメンバー、 [ **PTP\_ベンダー\_データ\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff546450)構造は無視されます。 ドライバーは、これらの正しい値を提供します。

エスケープ以外のベンダー定義コマンドの\_PTP\_クリア\_区画、特別なフラグをエスケープ\_PTP\_ベンダー\_コマンドを (OR 演算子を使用して) 組み合わせる必要があります、コマンドを使用使用される、 **IWiaItemExtras::Escape**メソッド。 ベンダー定義コマンドを作成するか、次の説明フラグを使用してデバイス上のオブジェクトを削除する場合、ドライバーは追加またはその内部構造からオブジェクトを削除し、WIA イベントが生成されます。 適切な WIA インターフェイスを通じて他のすべての標準コマンドを発行する必要があります。

最初のパラメーター **IWiaItemExtras::Escape**は、次のフラグの 1 つ以上の組み合わせです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エスケープ コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_CMD</p></td>
<td><p>オブジェクトが追加されると、オブジェクトのハンドルがコマンドのパラメーターのいずれか。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_CMD</p></td>
<td><p>オブジェクトが削除されると、オブジェクトのハンドルがコマンドのパラメーターのいずれか。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_RESP</p></td>
<td><p>オブジェクトが追加されると、オブジェクトのハンドルが応答のパラメーターのいずれか。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_RESP</p></td>
<td><p>オブジェクトが削除されると、オブジェクトのハンドルが応答のパラメーターのいずれか。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM1</p></td>
<td><p>コマンドまたは応答の最初のパラメーターが追加または削除されたオブジェクトのハンドルです。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM2</p></td>
<td><p>コマンドまたは応答の 2 番目のパラメーターが追加または削除されたオブジェクトのハンドルです。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM3</p></td>
<td><p>コマンドまたは応答の 3 番目のパラメーターが追加または削除されたオブジェクトのハンドルです。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM4</p></td>
<td><p>コマンドまたは応答の 4 番目のパラメーターが追加または削除されたオブジェクトのハンドルです。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM5</p></td>
<td><p>コマンドまたは応答の 5 番目のパラメーターが追加または削除されたオブジェクトのハンドルです。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_CLEAR_STALLS</p></td>
<td><p>ベンダー拡張コマンドによるエラー状態をオフにします。 このフラグは、他のフラグのいずれかと組み合わせて使用できません。 このフラグの詳細については、次の表の後の注を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_VENDOR_COMMAND</p></td>
<td><p>コマンドは、ベンダー拡張コマンドです。</p></td>
</tr>
</tbody>
</table>

 

**注**  アプリケーションを呼び出すと**IWiaItemExtras::Escape** 、エスケープ\_PTP\_クリア\_ドライバーには、このメソッドは、最初の引数として停止フラグ発行、PTP**デバイスの状態の取得**任意のエンドポイントは停止状態でかどうかを判断する要求。 場合、**デバイスの状態の取得**コマンドが成功すると、ドライバーの問題、 [ **IOCTL\_リセット\_パイプ**](https://msdn.microsoft.com/library/windows/hardware/ff542872)このような各エンドポイントの USB 制御コード。 場合、**デバイスの状態の取得**コマンドが失敗した、ドライバーが、PTP**デバイス リセット**要求。 **デバイスの状態を取得する**と**デバイス リセット**ピマ 15740:2000 標準、最初のエディション、およびリビジョン 1.0 USB まだイメージ キャプチャ デバイス定義の (USB SICDD) に記載されています。

 

次のサンプル コードは、コマンドのベンダー拡張インターフェイスを使用する方法を示しています。 コードが含まれているかどうかを必ず、 *ptpusd.h*ヘッダー エスケープ コードおよび他の定数の定義が含まれているため、および[ **PTP\_ベンダー\_データ\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff546450)と[ **PTP\_ベンダー\_データ\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff546452)構造体。 **IWiaItemExtras**インターフェイスがへの呼び出しを使用して取得した**QueryInterface**ルート項目にします。 このルート項目へのポインター *pIWiaRootItem*、取得できます、たとえばへの呼び出しによって**IWiaDevMgr::SelectDeviceDlg** (Microsoft Windows SDK のドキュメントで説明)。

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

 

 




