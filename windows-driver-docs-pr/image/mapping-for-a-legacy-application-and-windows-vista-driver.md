---
title: レガシ アプリケーションと Windows Vista ドライバーのマッピング
description: レガシ アプリケーションと Windows Vista ドライバーのマッピング
ms.assetid: 6f4ebcc7-ecf0-4e0b-bcef-e5b72dc472dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b771ae00a837fc269429617dbc61abc6c9f212
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840786"
---
# <a name="mapping-for-a-legacy-application-and-windows-vista-driver"></a>レガシ アプリケーションと Windows Vista ドライバーのマッピング


このセクションでは、レガシアプリケーションで Windows Vista ドライバーを使用する必要がある場合に、Windows Vista 転送メッセージとデータフローが従来の転送メッセージとデータフローにどのようにマップされるかについて説明します。

### <a name="callback-transfers"></a>コールバックの転送

次の表は、レガシアプリケーションに送信されるメッセージへの Windows Vista ドライバーのコールバックメッセージのマッピングを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista ドライバーメッセージ</strong></p></td>
<td><p><strong>レガシアプリケーションメッセージ (互換性レイヤー変換後)</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>無効.</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>無効. このメッセージは、常に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)"><strong>IwiatransGetNextStream callback::</strong></a>の呼び出しと共に表示されます。 メッセージが複製されていない場合は、 <strong>GetNextStream</strong>の実装で実装されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION (注 WIA_TRANSFER_MSG_END_OF_TRANSFER はドライバーによって送信されません)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>HrErrorStatus = = WIA_STATUS_WARMING_UP の場合、互換性レイヤーは、アプリケーションに何らかの状態を提供し、転送を取り消す可能性を Windows Vista アプリケーションに与えるために、IT_STATUS_TRANSFER_FROM_DEVICE と IT_MSG_STATUS を送信します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>無効. この場合、windows vista ドライバーで TYMED_FILE を使用してを呼び出すため、このドライバーからは送信しないでください。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback:: GetNextStream</strong></p></td>
<td><p>最初のページ: IT_MSG_DATA_HEADER</p>
<p>後続のページ: IT_MSG_NEW_PAGE</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream:: Write</strong></p></td>
<td><p>IT_MSG_DATA</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>ファイル転送

次の表は、レガシアプリケーションに送信されるメッセージへの Windows Vista ドライバーのファイル転送メッセージのマッピングを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista ドライバーメッセージ</strong></p></td>
<td><p><strong>レガシアプリケーションメッセージ (互換性レイヤー変換後)</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>無効.</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>無効. このメッセージは、常に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)"><strong>IwiatransGetNextStream callback::</strong></a>の呼び出しと共に表示されます。 メッセージが重複しないようにするために、このメッセージは<strong>GetNextStream</strong>の実装で実装されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION (注 WIA_TRANSFER_MSG_END_OF_TRANSFER はドライバーによって送信されません)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>HrErrorStatus = = WIA_STATUS_WARMING_UP の場合、IT_MSG_STATUS は IT_STATUS_TRANSFER_FROM_DEVICE と一緒に送信されます。これは、アプリケーションに何らかの状態を提供し、Windows Vista アプリケーションに転送を取り消す可能性を与えるためのものです。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>IT_MSG_NEW_PAGE</p>
<p>注: <em>wiasWritePageBufToFile</em>が IT_MSG_NEW_PAGE を送信することはないため、この動作は、現在、複数ページのファイル転送とは多少異なります。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback:: GetNextStream</strong></p></td>
<td><p>最初のページ: IT_MSG_FILE_PREVIEW_DATA_HEADER</p>
<p>後続ページ: エラー (WIA_ERROR_GENERAL_ERROR はドライバーに戻されます)。 <strong>Iwiatransfercallback:: GetNextStream</strong>を呼び出すことができるのは、TYMED_FILE を使用して1ページのみを転送でき、TYMED_MULTIPAGE_FILE 転送中は Windows Vista ドライバーが<strong>GetNextStream</strong>を呼び出す必要があるためです。ページは同じストリームに入る必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream:: Write</strong></p></td>
<td><p>メッセージは送信されませんでした。 ファイル転送の場合、ドライバー (画像処理フィルター) によって従来の転送メッセージに書き込まれるデータは、互換性レイヤーによって変換されません。 データは、転送の最後にユーザーに返されるファイルに単純に書き込まれます。</p></td>
</tr>
</tbody>
</table>

 

従来の転送メッセージの詳細については、「 [IWiaMiniDrvCallBack インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)」を参照してください。

TYMED 定数の詳細については、「 [TYMED](understanding-tymed.md)について」を参照してください。

**IStream**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

 

 




