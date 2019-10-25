---
title: WIA 転送定数
description: WIA 転送定数
ms.assetid: 69f76919-5bbb-4968-997c-2d51f19aab6b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53852889e9fea285928d576a3c1935e0b11648c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840667"
---
# <a name="wia-transfer-constants"></a>WIA 転送定数


このトピックには、WIA **IStream**ベースの転送に使用される定数の一覧が含まれています。

これらの定数は、次の3つのサブグループに分かれています。

-   項目の種類

-   コールバックメッセージ

-   転送フラグ

### <a name="item-type"></a>項目の種類

次の表は、ストリームベースのデータ転送に関連する WIA 項目の種類を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>この<a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_FLAGS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)"><strong>WIA_IPA_ITEM_FLAGS</strong></a>ビットは、データを転送できるすべての項目に対して設定する必要があります。つまり、このビットが設定されている項目に対して、アプリケーションがダウンロードまたはアップロードを開始できます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="callback-messages"></a>コールバックメッセージ

次の表は、 **Iwiatransfercallback:: transfercallback**の*lflags*パラメーターに使用できる値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>転送の進行状況をアプリケーションに通知します。</p>
<p><em>Pwiatransの params</em>-&gt; <em>lpercentcomplete</em>率には、この項目の完了率と転送されているページが含まれます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>現在のデータストリームに転送されるデータがなくなったこと、およびストリームが閉じられている可能性があることをアプリケーションに通知します。</p>
<p>その後、複数項目または複数ページの転送で、新しいストリームが要求される可能性があります。</p>
<p>ドライバーは、このメッセージを手動で送信しません。このメッセージは、ドライバーが次のストリームを要求したときに、自動的に送信されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>転送の最後にアプリケーションによって受信されます。</p>
<p>ドライバーはこのメッセージを送信しません。このメッセージは、転送が終了した後 (つまり、 <strong>IWiaMiniDrv::D rvacquiitemdata</strong>を呼び出すと)、WIA サービスによって自動的に送信されます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>将来使用するために Microsoft によって予約されています。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>転送中にエラーが発生したことを示します (紙詰まりなど)。</p>
<p><em>Pwiatransferparams</em>-&gt;<em>hrErrorStatus</em>には、エラー状態コードが含まれています。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>1つのファイル内の複数のページ (マルチファイル TIFF など) をサポートする形式が使用されている場合に、マルチページ転送中に新しいページが転送されることを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="transfer-flags"></a>転送フラグ

次の表は、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)に渡すことができるフラグを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_DOWNLOAD</p></td>
<td><p>転送がストリームベースのダウンロード操作 (つまり、デバイスからアプリケーションへのデータ転送) であることを示します。</p>
<p>アプリケーションでは、このビットを直接設定しません。 アプリケーションが<strong>IWiaTransfer::D o)</strong>を呼び出す場合、WIA サービスはこのビットを設定します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MINIDRV_TRANSFER_UPLOAD</p></td>
<td><p>転送がストリームベースのアップロード操作 (つまり、アプリケーションからデバイスへのデータ転送) であることを示します。</p>
<p>アプリケーションでは、このビットを直接設定しません。 アプリケーションが<strong>IWiaTransfer:: Upload</strong>を呼び出すと、WIA サービスはこのビットを設定します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN</p></td>
<td><p>ドライバーがフォルダー転送を実行する必要があることを示します。 この値がフォルダー項目で呼び出された場合、アプリケーションはそのフォルダーの子の転送を要求します。</p>
<p>この値は、 <strong>IWiaTransfer::D o)</strong>の<em>LFLAGS</em>パラメーターを<em>WIA _TRANSFER_ACQUIRE_CHILDREN に</em>設定することによって、アプリケーションがフォルダー転送を要求する場合に設定されます。ドライバーでは、複数の子を転送できるように指定されています。1つのスキャン。 ドライバーがこの種類の転送を実行できない場合、WIA サービスはドライバーに対して複数の呼び出しを行い、WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN は設定され<em>ません</em>。</p></td>
</tr>
</tbody>
</table>

 

**IWiaTransfer**および**Iwiatrancallback**インターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




