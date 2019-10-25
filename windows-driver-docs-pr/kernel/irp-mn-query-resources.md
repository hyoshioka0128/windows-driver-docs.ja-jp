---
title: IRP_MN_QUERY_RESOURCES
description: PnP マネージャーは、この IRP を使用して、デバイスのブート構成リソースを取得します。バスドライバーは、ハードウェアリソースを必要とする子デバイスに対して、この要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。
ms.date: 08/12/2017
ms.assetid: b9a6f06b-07d9-4539-bd41-21cdccdc4b25
keywords:
- IRP_MN_QUERY_RESOURCES カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: df4f147781b3311c10cf5a62bf42c589995d1fda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838567"
---
# <a name="irp_mn_query_resources"></a>IRP\_\_クエリ\_リソース


PnP マネージャーは、この IRP を使用して、デバイスのブート構成リソースを取得します。

バスドライバーは、ハードウェアリソースを必要とする子デバイスに対して、この要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスが列挙されたときにこの IRP を送信します。

PnP マネージャーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するバスドライバーは、 **irp&gt;iostatus. status**を STATUS\_SUCCESS または適切なエラー状態に設定します。

正常に完了すると、バスドライバーは、要求された情報を含む[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)へのポインターに、 **Irp&gt;iostatus**を設定します。 エラーが発生した場合、バスドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

<a name="operation"></a>操作
---------

バスドライバーは、この IRP に応答してリソースリストを返すと、ページメモリから[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)を割り当てます。 不要になったときに、PnP マネージャーによってバッファーが解放されます。

デバイスがハードウェアリソースを必要としない場合、デバイスの親バスドライバーは、 **irp&gt;IoStatus. Status**または**Irp-&gt;Iostatus. Information**を変更せずに、irp ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

関数ドライバーとフィルタードライバーは、この IRP を受信しません。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

ドライバーは、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出して、未加工のフォームと変換されたフォームの両方で、デバイスのブート構成を取得できます。

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


[**CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




