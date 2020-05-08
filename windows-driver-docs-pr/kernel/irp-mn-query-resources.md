---
title: IRP_MN_QUERY_RESOURCES
description: PnP マネージャーは、この IRP を使用して、デバイスのブート構成リソースを取得します。バスドライバーは、ハードウェアリソースを必要とする子デバイスに対して、この要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。
ms.date: 08/12/2017
ms.assetid: b9a6f06b-07d9-4539-bd41-21cdccdc4b25
keywords:
- IRP_MN_QUERY_RESOURCES カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: b55cd29d442dcb238f99741b273252162d02b407
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922563"
---
# <a name="irp_mn_query_resources"></a>IRP\_の\_全\_クエリリソース


PnP マネージャーは、この IRP を使用して、デバイスのブート構成リソースを取得します。

バスドライバーは、ハードウェアリソースを必要とする子デバイスに対して、この要求を処理する必要があります。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。

## <a name="value"></a>値

0x0A

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


この IRP を処理するバスドライバーは、 **irp&gt;-iostatus を設定します。** 状態は\_SUCCESS または適切なエラー状態に設定されます。

正常に完了すると、バスドライバーは、要求された情報を含む[**CM\_\_リソースリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)へのポインターに**Irp-&gt;iostatus**を設定します。 エラーが発生した場合、バスドライバーは**Irp-&gt;Iostatus. 情報**を0に設定します。

<a name="operation"></a>Operation
---------

この IRP に応答してバスドライバーがリソースリストを返す場合、ページメモリ[**から\_CM\_リソースリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)が割り当てられます。 不要になったときに、PnP マネージャーによってバッファーが解放されます。

デバイスがハードウェアリソースを必要としない場合、デバイスの親バスドライバーは、irp **-&gt;iostatus. Status**または**Irp-&gt;iostatus. INFORMATION**を変更せずに、irp ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

関数ドライバーとフィルタードライバーは、この IRP を受信しません。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

ドライバーは、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を呼び出して、未加工のフォームと変換されたフォームの両方で、デバイスのブート構成を取得できます。

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


[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




