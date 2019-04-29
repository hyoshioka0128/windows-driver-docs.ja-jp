---
title: IRP_MN_FILTER_RESOURCE_REQUIREMENTS
description: PnP マネージャーは、該当する場合、関数ドライバーが、デバイスに必要なリソースを調整することができますので、デバイス スタックをこの IRP を送信します。関数のドライバーは、通常、この IRP を処理します。
ms.date: 08/12/2017
ms.assetid: f43dc60e-de88-4af0-ad83-3ce3a414d880
keywords:
- IRP_MN_FILTER_RESOURCE_REQUIREMENTS カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 253b31f8aa8033c0318f2104d6812e2619eb8396
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391973"
---
# <a name="irpmnfilterresourcerequirements"></a>IRP\_MN\_フィルター\_リソース\_要件


PnP マネージャーは、該当する場合、関数ドライバーが、デバイスに必要なリソースを調整することができますので、デバイス スタックをこの IRP を送信します。

関数のドライバーは、通常、この IRP を処理します。

親バス ドライバー (およびフィルター ドライバーのバス) PDO; の子は、この要求を処理する必要があります。このようなドライバーが必要なリソースへの応答を報告する代わりに、 [ **IRP\_MN\_クエリ\_リソース\_要件**](irp-mn-query-resource-requirements.md)要求。

上限と下限フィルター ドライバーでは、この IRP は処理されません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスにリソースを割り当てる準備中であるときに、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッドのコンテキストでレベル。

## <a name="input-parameters"></a>入力パラメーター


**Irp -&gt;IoStatus.Information**を指す、 [ **IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)ハードウェアを含むデバイスのリソース要件。 ポインターが**NULL**場合は、デバイスがハードウェア リソースを消費しません。

**Parameters.FilterResourceRequirements.IoResourceRequirementList**も指す、 **IO\_リソース\_要件\_一覧**関数のドライバーを使用する必要がありますが、ボックスの一覧で、 **IoStatus**ブロックします。

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


関数のドライバーでは、この IRP を処理する場合、stack のバックアップ方法の IRP で処理します。 関数ドライバーは IRP を正常に処理する場合は設定**Irp -&gt;IoStatus.Status**ステータス\_成功とセット**Irp -&gt;IoStatus.Information**に、ポインター、 [ **IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)フィルター選択されたリソースの要件を格納しています。 フィルター選択されたリソース一覧の設定の詳細については、以下のセクション「操作」を参照してください。 関数のドライバーには、この IRP を処理するときにエラーが発生すると場合、、エラーは設定**Irp -&gt;IoStatus.Status**します。 関数のドライバーがこの IRP を処理しない場合は、使用[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355) IRP が下位のスタックを渡すには変更されません。

上限と下限フィルター ドライバーでは、この IRP は処理されません。 このようなドライバーを呼び出す**IoSkipCurrentIrpStackLocation**、次のドライバーに IRP を渡す、変更しないでください。 **Irp -&gt;IoStatus**、IRP を完了する必要があります。

親のバス ドライバーでは、この IRP を処理しません。 外に出て**Irp -&gt;IoStatus** IRP の完了であり。

<a name="operation"></a>操作
---------

PnP マネージャーに送信、 [ **IRP\_MN\_クエリ\_リソース\_要件**](irp-mn-query-resource-requirements.md)前に、デバイスの親バス ドライバーに要求します関数のドライバーでは、デバイス、そのオブジェクトをデバイス スタックにアタッチします。 PnP マネージャー機能ドライバーを該当する場合、デバイスのリソースの要件を変更する機会を提供、送信後、 **IRP\_MN\_フィルター\_リソース\_の要件**フル デバイス スタックを要求します。 PnP マネージャーは、デバイスの初期構成中に、デバイスにハードウェア リソースを割り当てる前に、この IRP を送信します。 PnP マネージャーは、リソースの再調整中にこの IRP を送信も可能性があります。

PnP マネージャーでは、この IRP を送信するときに、ドライバーを変更し、返すリソース要件リストを持つドライバー スタックを提供します。 PnP マネージャーでは、次の種類のリソース要件の一覧 (優先度の順序で表示) の 1 つは指定します。

-   強制の構成 (リソースの一覧からリソース要件のリストを変更)

-   構成をオーバーライドします。

-   基本構成

-   (リソースの一覧からリソース要件のリストを変更)、ブート構成

関数のドライバーでは、この IRP を処理する場合は完了ルーチンを設定する必要があり、バックアップ デバイス スタックを途中で IRP を処理します。 参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)バックアップ デバイス スタックを途中での PnP IRP の処理についてはします。

関数のドライバーによって示される現在の一覧のサイズに変化がない場合**Irp -&gt;IoStatus.Information**ドライバーは、場所の一覧を変更できます。 ドライバーの要件の一覧のサイズを変更する場合は、新しいドライバーを割り当てる必要があります[ **IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)からリスト ページメモリと、前述の一覧を解放します。 PnP マネージャーは、不要になったときに返される構造体を解放します。

関数のドライバーが指すリスト内のリソースの順序を維持する必要があります**Irp -&gt;IoStatus.Information**ハンドルされないリソースのタグを変更する必要があります。 ドライバーは、デバイスの親のバスをサポートする方法の要件リストを調整する注意する必要があります。 Function ドライバーの要件の一覧に新しいリソースを追加して、そのリソースがデバイスに割り当てられている場合、関数ドライバーはそのリソースのうちをフィルター処理する必要があります、 [ **IRP\_MN\_開始\_デバイス**](irp-mn-start-device.md)バス ドライバーまで開始 IRP を渡す前にします。

PnP マネージャーでリソースの要件を使用して、親のバス ドライバーへの応答で指定されたデバイスの機能のドライバーがこの IRP を処理しない場合、 [ **IRP\_MN\_クエリ\_リソース\_要件**](irp-mn-query-resource-requirements.md)要求。

関数のドライバーをドライバーの後にいつでもこの IRP のデバイスを処理するために準備する必要があります[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)デバイスのルーチンが呼び出されました。

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

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


[**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)

[**ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)

[**IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)

[**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)

 

 




