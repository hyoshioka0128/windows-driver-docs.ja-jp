---
title: IRP_MN_QUERY_RESOURCES
description: PnP マネージャーでは、この IRP を使用して、デバイスのブート構成リソースを取得します。バス ドライバーには、ハードウェア リソースを必要とされる子デバイスは、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。
ms.date: 08/12/2017
ms.assetid: b9a6f06b-07d9-4539-bd41-21cdccdc4b25
keywords:
- IRP_MN_QUERY_RESOURCES Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 04c023474cb8fbfcbb4f6ef232179f9c66a105f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370853"
---
# <a name="irpmnqueryresources"></a>IRP\_MN\_クエリ\_リソース


PnP マネージャーでは、この IRP を使用して、デバイスのブート構成リソースを取得します。

バス ドライバーには、ハードウェア リソースを必要とされる子デバイスは、この要求を処理する必要があります。 関数とフィルター ドライバーでは、この IRP は処理されません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスが列挙されたときに、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するバス ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態にします。

成功した場合、バス ドライバーの設定**Irp -&gt;IoStatus.Information**へのポインターを[ **CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list)を格納しています。要求された情報です。 バス ドライバーの設定エラーが発生、 **Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

割り当てるバス ドライバーでは、この IRP への応答でリソースの一覧が返された場合、 [ **CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list)ページングされたメモリから。 PnP マネージャーは、不要になったときにバッファーを解放します。

デバイスの親のバス ドライバーが IRP を完了すると、デバイスにないハードウェア リソースが必要とする場合 ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)) を変更しなくても**Irp-&gt;IoStatus.Status**または**Irp -&gt;IoStatus.Information**します。

関数とフィルター ドライバーは、この IRP を受信しません。

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

ドライバーを呼び出すことができます[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)生と翻訳の両方のフォームで、デバイスのブート構成を取得します。

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


[**CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)

 

 




