---
title: レガシ アプリケーションと Windows Vista ドライバーのマッピング
description: レガシ アプリケーションと Windows Vista ドライバーのマッピング
ms.assetid: 6f4ebcc7-ecf0-4e0b-bcef-e5b72dc472dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c711bb93cfd9d1b33f55ed46aa2a49f4fb4a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380387"
---
# <a name="mapping-for-a-legacy-application-and-windows-vista-driver"></a>レガシ アプリケーションと Windows Vista ドライバーのマッピング


このセクションでは、Windows Vista のメッセージの転送とデータ フローにマップする方法従来の転送メッセージとデータ フロー、レガシ アプリケーションは、Windows Vista ドライバーを使用する必要がある場合について説明します。

### <a name="callback-transfers"></a>コールバックの転送

この表では、レガシ アプリケーションに送信されるメッセージに、Windows Vista のドライバーのコールバックの転送メッセージのマッピングを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista ドライバー メッセージ</strong></p></td>
<td><p><strong>(互換性レイヤーの変換) した後、従来のアプリケーション メッセージ</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>無視されます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>無視されます。 このメッセージは常にへの呼び出しと共に送信されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff545039" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545039)"> <strong>IWiaTransferCallback::GetNextStream</strong></a>します。 すべてのメッセージを重複していない、これは実装、 <strong>GetNextStream</strong>実装代わりにします。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION (注 WIA_TRANSFER_MSG_END_OF_TRANSFER はドライバーによって送信されません)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>場合 hrErrorStatus WIA_STATUS_WARMING_UP、= = 互換性レイヤーをアプリケーションだけでなく、Windows Vista アプリケーションの可能性を与える、転送をキャンセルするいくつかの状態を提供するために IT_STATUS_TRANSFER_FROM_DEVICE で IT_MSG_STATUS を送信します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>無視されます。 送信しない Windows Vista のドライバーによってこの場合、TYMED_FILE で Windows Vista のドライバーに呼び出し以降。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback::GetNextStream</strong></p></td>
<td><p>最初のページ:IT_MSG_DATA_HEADER</p>
<p>後続のページ:IT_MSG_NEW_PAGE</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream::Write</strong></p></td>
<td><p>IT_MSG_DATA</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>ファイル転送

この表では、レガシ アプリケーションに送信されるメッセージに、Windows Vista のドライバーのファイルの転送メッセージのマッピングを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows Vista ドライバー メッセージ</strong></p></td>
<td><p><strong>(互換性レイヤーの変換) した後、従来のアプリケーション メッセージ</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>IT_MSG_STATUS</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>無視されます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>無視されます。 このメッセージは常にへの呼び出しと共に送信されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff545039" data-raw-source="[&lt;strong&gt;IWiaTransferCallback::GetNextStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545039)"> <strong>IWiaTransferCallback::GetNextStream</strong></a>します。 重複するメッセージを避けるためには、このメッセージが実装されている、 <strong>GetNextStream</strong>実装代わりにします。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>IT_MSG_TERMINATION (注 WIA_TRANSFER_MSG_END_OF_TRANSFER はドライバーによって送信されません)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>場合 hrErrorStatus WIA_STATUS_WARMING_UP、= = アプリケーションだけでなく、Windows Vista アプリケーションの可能性を与える転送をキャンセルするいくつかの状態を提供するために IT_MSG_STATUS は IT_STATUS_TRANSFER_FROM_DEVICE と共に送信されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>IT_MSG_NEW_PAGE</p>
<p>注: この動作は複数のページとは少し異なるために、このファイル転送を今すぐ<em>wiasWritePageBufToFile</em> IT_MSG_NEW_PAGE を送信しません。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaTransferCallback::GetNextStream</strong></p></td>
<td><p>最初のページ:IT_MSG_FILE_PREVIEW_DATA_HEADER</p>
<p>後続のページ:(、WIA_ERROR_GENERAL_ERROR をドライバーに返される) にエラーが発生しました。 <strong>IWiaTransferCallback::GetNextStream</strong>のみ、Windows Vista ドライバーを呼び出すのみ TYMED_FILE と TYMED_MULTIPAGE_FILE 転送中に 1 つのページ、転送できるため、後にのみ呼び出す<strong>GetNextStream</strong>したらため、すべてのページは、同じストリームに移動する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IStream::Write</strong></p></td>
<td><p>送信されたメッセージはありません。 ファイルの転送が発生した場合、互換性レイヤーは変換されません (イメージ処理 filter) ドライバーは、従来の転送メッセージに書き込みますデータのいずれか。 代わりに、データは単に転送の最後に、ユーザーに返されるファイルに書き込まれます。</p></td>
</tr>
</tbody>
</table>

 

詳細については、従来の転送でメッセージを参照してください、 [IWiaMiniDrvCallBack インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543943)します。

TYMED 定数の詳細については、次を参照してください。[理解 TYMED](understanding-tymed.md)します。

**IStream**インターフェイスは、Microsoft Windows SDK ドキュメントで説明します。

 

 




