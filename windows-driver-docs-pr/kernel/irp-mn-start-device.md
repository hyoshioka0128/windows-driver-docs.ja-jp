---
title: IRP_MN_START_DEVICE
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 0aac1346-b5c7-4dcc-ab86-03e8fd151505
keywords:
- IRP_MN_START_DEVICE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: ff9e11350d5677f252c1a84ac90eaaf71039733b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381400"
---
# <a name="irpmnstartdevice"></a>IRP\_MN\_開始\_デバイス


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスに存在する場合は、ハードウェア リソースが割り当てられるこの IRP を送信します。 デバイスが最近列挙され、は、最初の起動中またはリソースが再調整のために停止した後は、デバイスを再起動する可能性があります。

PnP マネージャーが送信することがあります、 **IRP\_MN\_開始\_デバイス**既に開始されているデバイスにデバイスが現在使用してよりに異なる一連のリソースを指定します。 ドライバーは、呼び出すことによってこの操作を開始する[ **IoInvalidateDeviceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549361)とそれに続く対応[ **IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](irp-mn-query-pnp-device-state.md) PNP 要求\_リソース\_要件\_CHANGED フラグを設定します。 バス ドライバーは PCI の PCI ブリッジで新しい aperture を開くなど、このメカニズムを使用可能性があります。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.StartDevice.AllocatedResources**のメンバー、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659) を指す構造体[ **CM\_リソース\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff541994) PnP マネージャーがデバイスに割り当てられたハードウェア リソースを記述します。 この一覧には、未加工の形式でリソースが含まれています。 生のリソースを使用して、デバイスをプログラミングします。

**Parameters.StartDevice.AllocatedResourcesTranslated**を指す、 [ **CM\_リソース\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff541994)ハードウェア リソースを記述するを PnP マネージャーデバイスに割り当てられます。 この一覧には、翻訳された形式でリソースが含まれています。 翻訳されたリソースを使用して、割り込みのベクターを接続し、I/O の領域をマップし、メモリをマップします。

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などの適切なエラー状態に\_失敗またはステータス\_不十分\_リソース。

ドライバーは、デバイスの場合は、その開始操作を実行すると時間を必要とする場合、保留中の IRP のマークし、状態を返す\_保留します。

<a name="operation"></a>操作
---------

この IRP は、デバイスの親のバス ドライバー、続いてデバイス スタックの各以上のドライバー最初に処理する必要があります。

この IRP への応答、ドライバーは、最初にデバイスを起動または停止していたデバイスを再起動します。 デバイスを起動するために必要な操作は、デバイスからデバイスへの変更が、デバイスの電源を入れて、デバイス固有の初期化を実行して、割り込みの接続を含めることができます。

ドライバーは、通常が最初にデバイスを起動または後にデバイスを再起動するかどうかと同じ方法でこの IRP を処理できる、 [ **IRP\_MN\_停止\_デバイス**](irp-mn-stop-device.md)、ドライバーは、停止した後、再起動時にデバイスの状態を復元する必要がある場合を除きます。

Windows Vista およびそれ以降のオペレーティング システムでは、ことをお勧めドライバー保留常に、 **IRP\_MN\_開始\_デバイス**IRP 後でその処理を完了します。 この順序により、デバイスの再起動を非同期に処理するシステムです。 (Windows Vista より前に、のオペレーティング システムでは、ドライバーが状態を返すことができます\_PENDING からは、ディスパッチ ルーチンが PnP マネージャーには、他の操作と、デバイスの再起動が重複していない)。

開始 IRP の処理の詳細については、次を参照してください。[デバイスを起動](https://msdn.microsoft.com/library/windows/hardware/ff563849)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_MN\_停止\_デバイス**](irp-mn-stop-device.md)

 

 




