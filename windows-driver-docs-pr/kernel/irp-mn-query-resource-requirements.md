---
title: IRP_MN_QUERY_RESOURCE_REQUIREMENTS
description: PnP マネージャーは、この IRP を使用して、デバイスのリソース要件の一覧を取得します。バスドライバーは、ハードウェアリソースを必要とする子デバイスに対して、この要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5a77f8d6-2b6b-4eff-8d48-e7942976ec52
keywords:
- IRP_MN_QUERY_RESOURCE_REQUIREMENTS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 2e42098dd6e7869e0e562bbcca7b756f8e86ed9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827987"
---
# <a name="irp_mn_query_resource_requirements"></a>IRP\_\_クエリ\_リソース\_の要件


PnP マネージャーは、この IRP を使用して、デバイスのリソース要件の一覧を取得します。

バスドライバーは、ハードウェアリソースを必要とする子デバイスに対して、この要求を処理する必要があります。 バスフィルタードライバーは、この要求を処理できます。 関数ドライバーとフィルタードライバーは、この IRP を処理しません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスが列挙されたとき、デバイスにリソースを割り当てる前、およびドライバーがそのデバイスのリソース要件を変更したことを報告したときに、この IRP を送信します。

PnP マネージャーは、任意のスレッドコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するドライバーは、 **irp&gt;iostatus**を、STATUS\_SUCCESS または適切なエラー状態に設定します。

成功すると、ドライバーは**Irp&gt;IoStatus. 情報**を、要求された情報を含む[**IO\_リソース\_要件\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)へのポインターに設定します。 エラーが発生した場合、ドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

<a name="operation"></a>操作
---------

この IRP に応答してバスドライバーがリソース要件の一覧を返す場合は、ページングされたメモリから **\_一覧の IO\_リソース\_要件**を割り当てます。 不要になったときに、PnP マネージャーによってバッファーが解放されます。

デバイスにハードウェアリソースが必要ない場合、デバイスのバスドライバーは、 **irp&gt;IoStatus. Status**または**Irp-&gt;Iostatus. Information**を変更せずに、irp ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) を完了します。

バスフィルタードライバーがこの IRP を処理する場合は、バスドライバーによって作成されたリソース要件の一覧を変更します。 バスフィルタードライバーは、IRP によってデバイススタックがバックアップされるように一覧を変更します。 バスフィルタードライバーはリソース要件の一覧にリソースの順序を保持する必要があり、処理しないリソースタグは変更できません。 バスフィルタードライバーがリソース要件の一覧のサイズを変更する場合、ドライバーはページングされたメモリから新しい構造体を割り当てて、前の構造体を解放する必要があります。 バスフィルタードライバーによって新しいリソース要件がリストに追加され、そのリソースがデバイスに割り当てられている場合、ドライバーはバスドライバーに渡されないように、Irp から新しいリソースをフィルター処理して\_デバイスの irp を[**開始\_\_** ](irp-mn-start-device.md)する必要があります。

関数および非バスフィルタードライバーは、この IRP を処理しません。**Irp&gt;IoStatus**を変更せずに、次の下位のドライバーに渡します。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

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


[**IO\_リソース\_要件\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)

 

 




