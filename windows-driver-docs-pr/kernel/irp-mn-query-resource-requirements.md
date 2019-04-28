---
title: IRP_MN_QUERY_RESOURCE_REQUIREMENTS
description: PnP マネージャーでは、この IRP を使用して、デバイスのリソース要件の一覧を取得します。バス ドライバーには、ハードウェア リソースを必要とされる子デバイスは、この要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5a77f8d6-2b6b-4eff-8d48-e7942976ec52
keywords:
- IRP_MN_QUERY_RESOURCE_REQUIREMENTS カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 905339d2b240448ba692195903933eac781fed71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381423"
---
# <a name="irpmnqueryresourcerequirements"></a>IRP\_MN\_クエリ\_リソース\_要件


PnP マネージャーでは、この IRP を使用して、デバイスのリソース要件の一覧を取得します。

バス ドライバーには、ハードウェア リソースを必要とされる子デバイスは、この要求を処理する必要があります。 バス フィルター ドライバーは、この要求を処理できます。 関数とフィルター ドライバーでは、この IRP は処理されません。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーは、デバイスにリソースを割り当てる前に、デバイスが列挙されたときに、ドライバーは、そのデバイスのリソース要件が変更されたことを報告したときに、この IRP を送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


状態の I/O ブロックで返されます。

## <a name="io-status-block"></a>I/O ステータス ブロック


この IRP を処理するドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功またはエラーを適切な状態です。

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**へのポインター、 [ **IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)要求された情報を格納します。 ドライバーの設定エラーが発生、 **Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

割り当てるバス ドライバーでは、この IRP への応答でリソースの要件の一覧が返された場合、 **IO\_リソース\_要件\_一覧**ページングされたメモリから。 PnP マネージャーは、不要になったときにバッファーを解放します。

デバイスのバス ドライバーが IRP を完了すると、デバイスには、ハードウェア リソースは必要ない場合、([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) を変更しなくても**Irp-&gt;IoStatus.Status**または**Irp -&gt;IoStatus.Information**します。

バスのフィルター ドライバーは、この IRP を処理する場合は、バス ドライバーで作成したリソースの要件のリストが変更されます。 バスのフィルター ドライバーは IRP デバイス stack のバックアップ方法の一覧を変更します。 Bus フィルター ドライバーは、リソース要件の一覧内のリソースの順序を維持する必要があり、ハンドルされないリソースのタグを変更する必要があります。 Bus フィルター ドライバーには、リソース要件の一覧のサイズが変更された場合、ドライバーはページングされたメモリから、新しい構造体を割り当てし、前の構造体を解放する必要があります。 ドライバーでの新しいリソースをフィルター処理する必要があります bus フィルター ドライバーは、新しいリソース要件を一覧に追加リソースがデバイスに割り当てられている場合は、 [ **IRP\_MN\_開始\_デバイス**](irp-mn-start-device.md) IRP バス ドライバーが渡されないようにします。

関数と非 bus フィルター ドライバー; この IRP を処理しません。[次へ] の下位のドライバーに変更を加えるに渡される**Irp -&gt;IoStatus**します。

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


[**IO\_リソース\_要件\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff550609)

 

 




