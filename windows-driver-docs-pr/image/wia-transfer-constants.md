---
title: WIA 転送定数
description: WIA 転送定数
ms.assetid: 69f76919-5bbb-4968-997c-2d51f19aab6b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbd778f1d426f9678b9af52e723f2ca0ea725836
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550641"
---
# <a name="wia-transfer-constants"></a>WIA 転送定数


このトピックでは、WIA に使用される定数の一覧を含む**IStream**-ベースの転送。

これらの定数は、3 つのサブグループに分類されます。

-   項目の種類

-   コールバック メッセージ

-   転送フラグ

### <a name="item-type"></a>項目の種類

次の表はどの WIA 項目型のビットは、ストリーム ベースのデータ転送に関連します。

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
<td><p>これは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551585" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_FLAGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551585)"> <strong>WIA_IPA_ITEM_FLAGS</strong> </a>ビットは、データを転送することができるすべての項目で設定する必要があります。 は、アプリケーションをダウンロードを開始またはことには、このビット セットのアイテムをアップロードできます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="callback-messages"></a>コールバック メッセージ

次の表に、使用可能な値の*lFlags*パラメーターの**IWiaTransferCallback::TransferCallback**します。

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
<td><p>転送の進行状況のアプリケーションに通知します。</p>
<p><em>pWiaTransferParams</em> - &gt; <em>lPercentComplete</em>このアイテムは、転送されているページの達成率が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>現在のデータ ストリームに転送するデータがあることと、ストリームを閉じることができます、アプリケーションに通知します。</p>
<p>複数項目または複数の転送に、新しいストリームを要求後場合があります。</p>
<p>ドライバー メッセージを送信しないこの - 手動で、WIA、ドライバーは、次のストリームを要求時に、サービスにこのメッセージは送信自動的にします。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>転送の終了時に、アプリケーションで受信します。</p>
<p>ドライバーは、--このメッセージの WIA を送信できませんはサービスがこのメッセージを自動的に送信、転送が終了した後 (への呼び出しは、 <strong>IWiaMiniDrv::drvAcquiItemData</strong>返します)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>将来使用するために Microsoft によって予約されています。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>(たとえば、紙詰まり)、転送中にエラーを示します。</p>
<p><em>pWiaTransferParams</em>-&gt;<em>hrErrorStatus</em>エラー ステータス コードが含まれています。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>1 つのファイル (マルチファイル TIFF) などの複数のページをサポートする形式が使用されているときに、新しいページが複数ページの転送中に転送されていることを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="transfer-flags"></a>転送フラグ

次の表に渡すことのできるフラグ[ **IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)します。

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
<td><p>転送が、ダウンロードのストリーム ベースの操作 (つまり、データ転送、デバイスからアプリケーションに) であることを示します。</p>
<p>アプリケーションでは、このビットを直接設定しないでください。 WIA サービスは、アプリケーションから呼び出す場合にこのビットを設定<strong>IWiaTransfer::Download</strong>します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MINIDRV_TRANSFER_UPLOAD</p></td>
<td><p>転送はストリーム ベースのアップロード操作 (デバイスにアプリケーションからのデータ転送) であることを示します。</p>
<p>アプリケーションでは、このビットを直接設定しないでください。 WIA サービスは、アプリケーションから呼び出す場合にこのビットを設定<strong>IWiaTransfer::Upload</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN</p></td>
<td><p>ドライバーをフォルダーの転送を実行することを示します。 この値は、フォルダー アイテムで呼び出されると、そのフォルダーの子を転送するアプリケーションを要求します。</p>
<p>アプリケーションを設定して、フォルダーの転送を要求する場合は、この値を設定するが、 <em>lFlags</em>パラメーターの<strong>IWiaTransfer::Download</strong> WIA _TRANSFER_ACQUIRE_CHILDREN に<em>と</em>ドライバーが 1 つのスキャンで複数の子要素を転送できることを指定します。 ドライバーは、この種類の転送を実行できません WIA サービスは、ドライバーに複数の呼び出しを行い、WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN は場合<em>いない</em>を設定します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、 **IWiaTransfer**と**IWiaTransferCallback**インターフェイス、Microsoft Windows SDK のドキュメントを参照してください。

 

 




