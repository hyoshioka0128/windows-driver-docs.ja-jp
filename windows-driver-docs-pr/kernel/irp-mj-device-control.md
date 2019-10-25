---
title: IRP_MJ_DEVICE_CONTROL
description: 特定のデバイスの種類に属するデバイスオブジェクトを持つすべてのドライバー (デバイスの種類の指定に関する記事を参照) は、システム定義の i/o 制御コード (Ioctl) のセットがその型に存在する場合に、DispatchDeviceControl ルーチンでこの要求をサポートするために必要です。
ms.date: 08/12/2017
ms.assetid: c6436b34-22bd-4e65-bfb0-b2c4d9962e29
keywords:
- IRP_MJ_DEVICE_CONTROL カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 5285556f92b324d3d9e708f10e34881a2ef2156e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838607"
---
# <a name="irp_mj_device_control"></a>IRP\_MJ\_DEVICE\_CONTROL


特定のデバイスの種類に属するデバイスオブジェクトを持つすべてのドライバー ([デバイスの種類の指定](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-types)に関する記事を参照) は、その型に対してシステム定義 i/o 制御コード (ioctl) のセットが存在する場合、 [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでこの要求をサポートするために必要です. Ioctl の詳細については、「 [I/o 制御コードの概要](introduction-to-i-o-control-codes.md)」を参照してください。

上位レベルのドライバーは、通常、これらの要求を基になるデバイスドライバーに渡します。 ドライバースタック内の各デバイスドライバーは、デバイスの種類固有のパブリックまたはプライベート Ioctl のセットと共に、この要求をサポートすることを前提としています。 特定のデバイスの種類の Ioctl の詳細については、「Microsoft Windows Driver Kit (WDK)」の「デバイスの種類に固有のドキュメント」を参照してください。

<a name="when-sent"></a>送信時
---------

作成要求が正常に完了した後、いつでも実行できます。

## <a name="input-parameters"></a>入力パラメーター


I/o 制御コードは、 **DeviceIoControl**に含まれています。これは、IRP のドライバーの i/o スタックの場所にあります。

その他の入力パラメーターは、i/o 制御コードの値によって異なります。 詳細については、「 [I/o 制御コードのバッファーの説明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)」を参照してください。

## <a name="output-parameters"></a>出力パラメーター


出力パラメーターは、i/o 制御コードの値によって異なります。 詳細については、「 [I/o 制御コードのバッファーの説明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)」を参照してください。

<a name="operation"></a>操作
---------

ユーザーモードスレッドが Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出したか、または上位レベルのカーネルモードドライバーが要求を設定したため、ドライバーはこの i/o 制御コードを受信します。 場合によっては、ユーザーモードドライバーが**DeviceIoControl**を呼び出して、ドライバーによって定義された (*プライベート*) i/o 制御コードを渡して、デバイスまたはドライバーに固有のカーネルモードデバイスドライバーからのサポートを要求します。

デバイス i/o 制御要求が受信されると、より高いレベルのドライバーは、通常、IRP を次の下位のドライバーに渡します。 ただし、この方法にはいくつかの例外があります。 たとえば、基になるポートドライバーから取得した構成情報が保存されているクラスドライバーは、対応するポートドライバーに IRP を渡さずに、特定の IOCTL\_*XXX*要求を完了させることができます。

デバイスドライバーは、デバイス i/o 制御要求の受信時に、要求を満たす方法を決定するために i/o 制御コードを調べます。 ほとんどのパブリック i/o 制御コードでは、デバイスドライバーが**Irp-&gt;AssociatedIrp**のバッファーとの間で少量のデータを転送します。

Irp\_MJ の i/o 制御コードに関する一般的な情報については **\_デバイス\_control**または[**irp\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)要求の場合は、「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」を参照してください。 「[デバイスの種類に固有の I/o 要求](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-type-specific-i-o-requests)」も参照してください。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




