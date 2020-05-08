---
title: IRP_MN_FILTER_RESOURCE_REQUIREMENTS
description: PnP マネージャーは、この IRP をデバイススタックに送信します。これにより、必要に応じて、関数ドライバーがデバイスに必要なリソースを調整できるようになります。関数ドライバーは通常、この IRP を処理します。
ms.date: 08/12/2017
ms.assetid: f43dc60e-de88-4af0-ad83-3ce3a414d880
keywords:
- IRP_MN_FILTER_RESOURCE_REQUIREMENTS カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 4ba8403da860416fa88f8487ffd028c7486df06f
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922485"
---
# <a name="irp_mn_filter_resource_requirements"></a>IRP\_の\_全\_フィルター\_のリソース要件


PnP マネージャーは、この IRP をデバイススタックに送信します。これにより、必要に応じて、関数ドライバーがデバイスに必要なリソースを調整できるようになります。

関数ドライバーは通常、この IRP を処理します。

親バスドライバー (およびバスフィルタードライバー) は、子 PDO に対するこの要求を処理することはできません。代わりに、このようなドライバーでは、 [**IRP\_\_の\_クエリリソース\_要件**](irp-mn-query-resource-requirements.md)要求に応じてリソース要件を報告する必要があります。

上位フィルターと下位フィルタードライバーは、この IRP を処理しません。

## <a name="value"></a>値

0x0D

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスにリソースを割り当てる準備をしているときに、この IRP を送信します。

PnP マネージャーは、任意のスレッドのコンテキスト\_で、この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Irp-&gt;Iostatus。情報**は、デバイスのハードウェアリソース要件を含む[**IO\_リソース\_\_要件の一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)を指します。 デバイスがハードウェアリソースを消費しない場合、ポインターは**NULL**になります。

**IoResourceRequirementList**は、FilterResourceRequirements も**\_IO リソース\_要件\_の一覧**を指しますが、関数ドライバーは**iostatus**ブロックの一覧を使用する必要があります。

## <a name="output-parameters"></a>出力パラメーター


I/o 状態ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


関数ドライバーがこの IRP を処理する場合、IRP がスタックをバックアップする方法で処理します。 関数ドライバーが IRP を正常に処理すると、 **irp-&gt;Iostatus. status**が\_SUCCESS に設定され、 **irp-&gt;iostatus. 情報**が、フィルター処理されたリソース要件を含む[**IO\_リソース\_要件\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)へのポインターに設定されます。 フィルター選択されたリソースリストの設定の詳細については、後述の「操作」セクションを参照してください。 この IRP を処理するときに関数ドライバーがエラーを検出した場合、 **irp-&gt;Iostatus. status**のエラーが設定されます。 関数ドライバーがこの IRP を処理しない場合は、 [**Ioskipを**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)使用して、irp をそのままスタックに渡します。

上位フィルターと下位フィルタードライバーは、この IRP を処理しません。 このようなドライバーは、 **Ioskipfinalentiの場所**を呼び出し、次のドライバーに irp を渡します。 irp **-&gt;iostatus**を変更することはできません。また、irp を完了することはできません。

親バスドライバーは、この IRP を処理しません。 **Irp-&gt;iostatus**はそのままで、irp を完了します。

<a name="operation"></a>Operation
---------

PnP マネージャーは、 [**IRP\_を使用\_し\_た\_クエリリソース要件**](irp-mn-query-resource-requirements.md)要求をデバイスの親バスドライバーに送信してから、関数ドライバーがデバイスオブジェクトをデバイススタックに接続します。 必要に応じて、関数ドライバーにデバイスのリソース要件を変更する機会を与えるために、PnP マネージャーは、後で**\_IRP\_\_\_** がいっぱいになったことを示すフィルターリソース要件要求を完全なデバイススタックに送信します。 PnP マネージャーは、初期デバイス構成中にハードウェアリソースをデバイスに割り当てる前に、この IRP を送信します。 PnP マネージャーは、リソースの再調整中にこの IRP を送信することもあります。

PnP マネージャーは、この IRP を送信するときに、ドライバースタックにリソース要件の一覧を提供します。ドライバーは、変更して返すことができます。 PnP マネージャーは、次のいずれかの種類のリソース要件一覧を提供します (優先順位順に記載)。

-   強制構成 (リソースリストからリソース要件リストに変更)

-   構成をオーバーライドする

-   基本構成

-   ブート構成 (リソースリストからリソース要件リストに変更)

関数ドライバーがこの IRP を処理する場合は、完了ルーチンを設定し、デバイススタックをバックアップするように IRP を処理する必要があります。 デバイススタックをバックアップするように PnP IRP を処理する方法については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

関数ドライバーが現在のリストのサイズを変更していない場合 ( **Irp-&gt;Iostatus. 情報**)、ドライバーは、その場でリストを変更できます。 ドライバーが要件の一覧のサイズを変更する必要がある場合、ドライバーはページングされたメモリから新しい[**IO\_\_リソース要件\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)リストを割り当てて、前の一覧を解放する必要があります。 不要になった場合は、返された構造体が PnP マネージャーによって解放されます。

関数ドライバーは、 **Irp-&gt;iostatus**によって示されるリスト内のリソースの順序を保持する必要があります。また、処理されないリソースタグを変更することはできません。 ドライバーは、デバイスの親バスがサポートする方法で要件の一覧を調整する必要があります。 関数ドライバーによって新しいリソースが要件の一覧に追加され、そのリソースがデバイスに割り当てられている場合、関数ドライバーは start IRP をバスドライバーに渡す前に、 [**irp\_\_が\_開始するデバイス**](irp-mn-start-device.md)からそのリソースをフィルター処理する必要があります。

デバイスの関数ドライバーがこの IRP を処理しない場合は、 [**irp\_\_の\_クエリリソース\_要件**](irp-mn-query-resource-requirements.md)の要求に応じて、親バスドライバーによって指定されたリソース要件が PnP マネージャーによって使用されます。

デバイスに対してドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが呼び出された後、いつでもこの IRP を処理できるように、関数ドライバーを準備する必要があります。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

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


[**Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)

[**IO\_リソース\_要件\_の一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)

[**IRP\_の\_全\_開始デバイス**](irp-mn-start-device.md)

 

 




