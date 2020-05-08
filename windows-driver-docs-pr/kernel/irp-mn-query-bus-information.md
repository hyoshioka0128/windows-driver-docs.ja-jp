---
title: IRP_MN_QUERY_BUS_INFORMATION
description: PnP マネージャーは、この IRP を使用して、デバイスの親バスの種類とインスタンス番号を要求します。バスドライバーは、子デバイス (PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。
ms.date: 08/12/2017
ms.assetid: a7ea1a81-7f03-41c7-8861-a2e1813c15cf
keywords:
- IRP_MN_QUERY_BUS_INFORMATION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: a8f907412ff25322391167271f06877a4dc252ab
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922575"
---
# <a name="irp_mn_query_bus_information"></a>IRP\_の\_全\_クエリ\_バス情報


PnP マネージャーは、この IRP を使用して、デバイスの親バスの種類とインスタンス番号を要求します。

バスドライバーは、子デバイス (PDOs) に対してこの要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。

## <a name="value"></a>値

0x15

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスが列挙されたときにこの IRP を送信します。

PnP マネージャーは、任意のスレッドコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


バスドライバーは、 **Irp-&gt;iostatus**を、状態\_が SUCCESS または適切なエラー状態に設定します。

正常に実行された場合、バスドライバーは**Irp-&gt;Iostatus. 情報**を、完了した[**\_PNP バス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)構造へのポインターに設定します。 (詳細については、「操作」セクションを参照してください)。エラーが発生した場合、バスドライバーは**Irp-&gt;Iostatus. 情報**を0に設定します。

関数ドライバーとフィルタードライバーは、この IRP を処理しません。

<a name="operation"></a>Operation
---------

この IRP への応答として返される情報は、バス上のデバイスの関数とフィルタードライバーで使用できます。 関数とフィルタードライバーは[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出して、 **Devicepropertybustypeguid**、 **DevicePropertyLegacyBusType**、または**devicepropertybusnumber**を要求できます。 複数のバス上のデバイスをサポートする関数とフィルタードライバーは、この情報を使用して、特定のデバイスがどのバスに存在するかを判断できます。

バスドライバーは、この IRP に応答して情報を返す場合、ページングされたメモリから**\_PNP バス\_情報**構造体を割り当てます。 不要になったときに、PnP マネージャーによって構造が解放されます。

**\_PNP バス\_情報**の構造体の形式は次のとおりです。

```cpp
typedef struct _PNP_BUS_INFORMATION {
    GUID BusTypeGuid;
    INTERFACE_TYPE LegacyBusType;
    ULONG BusNumber;
} PNP_BUS_INFORMATION, *PPNP_BUS_INFORMATION;
```

構造体のメンバーは、次のように定義されます。

<a href="" id="bustypeguid"></a>**BusTypeGuid**  
バスドライバーは、デバイスが存在するバスの種類の GUID に**Bustypeguid**を設定します。 標準バスタイプの Guid は、Wdmguid. h に記載されています。 ドライバーの作成者は、Uuidgen.exe を使用して他の種類のバスの Guid を生成する必要があります。

<a href="" id="legacybustype"></a>**LegacyBusType**  
PnP バスドライバーは、 **LegacyBusType**を親バスの[**インターフェイス\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_interface_type)に設定します。 インターフェイスの種類は、Wdm で定義されています。 一部のバスには、特定の**インターフェイス\_の種類**の値 ( **PCMCIABus**、 **PCIBus**、 **PNPISABus**など) があります。 他のバス、特に新しいバス (USB など) の場合、バスドライバーはこのメンバーを**PNPBus**に設定します。

**LegacyBusType**は、デバイスとの通信に使用するインターフェイスを指定します。 これは、親バスの種類に対応している場合もあれば、対応していない場合もあります。 たとえば、PCI CardBus コントローラーに接続されている CardBus カードのインターフェイスは、 **PCIBus**です。 ただし、PCI CardBus コントローラー上の PCMCIA カードのインターフェイスは**PCMCIABus**です。

<a href="" id="busnumber"></a>**BusNumber**  
バスドライバーは、 **Busnumber**を、コンピューター上の同じ種類の他のバスと区別する数値に設定します。 バス番号付けスキームはバス固有です。 バス番号は仮想にすることができますが、 [**IoReportResourceUsage**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)などの従来のインターフェイスで使用されている番号と一致する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出して、デバイスが接続されているバスに関する情報を取得します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




