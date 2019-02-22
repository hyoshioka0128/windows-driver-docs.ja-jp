---
title: IRP_MJ_DEVICE_CONTROL
description: 型の一連のシステム定義されている I/O 制御コード (Ioctl) が存在する場合、すべてのドライバーの特定のデバイスが (デバイスの種類の指定を参照してください) を入力するオブジェクトが属しているデバイスは DispatchDeviceControl ルーチンで、この要求をサポートする必要があります。
ms.date: 08/12/2017
ms.assetid: c6436b34-22bd-4e65-bfb0-b2c4d9962e29
keywords:
- IRP_MJ_DEVICE_CONTROL カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: e495c1b63ed6f37115e0381dad9867c5eb6cabbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531750"
---
# <a name="irpmjdevicecontrol"></a>IRP\_MJ\_デバイス\_コントロール


デバイス オブジェクトが特定のデバイスの種類に属するすべてのドライバー (を参照してください[デバイスの種類の指定](https://msdn.microsoft.com/library/windows/hardware/ff563821)) では、この要求をサポートするために必要な[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)型の一連のシステム定義の I/O 制御コード (Ioctl) 場合、ルーチンが存在します。 Ioctl に関する詳細については、次を参照してください。 [I/O 制御コードの概要](introduction-to-i-o-control-codes.md)します。

高度なドライバーは、通常は、基になるデバイス ドライバーにこれらの要求を渡します。 ドライバー スタックでは、各デバイス ドライバーは、一連のデバイスの種類に固有でパブリックまたはプライベートの Ioctl と共に、この要求をサポートすると見なされます。 特定のデバイスの種類の Ioctl の詳細については、Microsoft Windows Driver Kit (WDK) でデバイスの型固有のドキュメントを参照してください。

<a name="when-sent"></a>送信時
---------

いつの作成要求が正常に完了します。

## <a name="input-parameters"></a>入力パラメーター


I/O 制御コードが含まれている**Parameters.DeviceIoControl.IoControlCode**ドライバーの I/O の IRP の場所をスタックします。

その他の入力パラメーターは、I/O 制御コードの値によって異なります。 詳細については、次を参照してください。 [I/O 制御コードの説明をバッファー](https://msdn.microsoft.com/library/windows/hardware/ff540663)します。

## <a name="output-parameters"></a>出力パラメーター


出力パラメーターは、I/O 制御コードの値によって異なります。 詳細については、次を参照してください。 [I/O 制御コードの説明をバッファー](https://msdn.microsoft.com/library/windows/hardware/ff540663)します。

<a name="operation"></a>操作
---------

ドライバーがユーザー モード スレッドには、Microsoft Win32 が呼び出されるために、この I/O 制御コードを受け取る[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)関数、またはより高度なカーネル モード ドライバーが要求を設定します。 場合によっては、ユーザー モード ドライバーが呼び出されて**DeviceIoControl**ドライバー定義を渡して、(とも呼ばれる*プライベート*) 密接に結合からデバイスまたはドライバーに固有のサポートを要求する、I/O 制御コードカーネル モード デバイス ドライバー。

デバイスの I/O 制御要求の受信後より高度なドライバーは通常、次の下位ドライバーに IRP を渡します。 ただし、この方針にいくつかの例外もあります。 たとえば、基になるポート ドライバーから取得した構成情報が格納されているクラス ドライバーは特定 IOCTL 可能性があります完了\_*XXX*ポートに対応するドライバーに IRP を渡さずに要求.

デバイスの I/O 制御要求の受信後、デバイス ドライバーは、要求を満たす方法を決定する I/O 制御コードを調べます。 デバイス ドライバーが少量のデータとの間でバッファーを転送するほとんどのパブリックの I/O 制御コードの**Irp -&gt;AssociatedIrp.SystemBuffer**します。

I/O に関する一般的な情報のコードを制御**IRP\_MJ\_デバイス\_コントロール**または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)要求を参照してください[I/O 制御コードを使用して](https://msdn.microsoft.com/library/windows/hardware/ff565406)します。 参照してください[デバイスの種類に固有の I/O 要求](https://msdn.microsoft.com/library/windows/hardware/ff543205)します。

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


[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




