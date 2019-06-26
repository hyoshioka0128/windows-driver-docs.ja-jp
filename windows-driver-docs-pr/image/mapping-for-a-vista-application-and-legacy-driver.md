---
title: Vista アプリケーションとレガシ ドライバーのマッピング
description: Vista アプリケーションとレガシ ドライバーのマッピング
ms.assetid: 176157b0-cc30-467b-95ec-2d25a40c43ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 399fc92bd60e01d0f0897ea285ec86ed3e017e4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378844"
---
# <a name="mapping-for-a-vista-application-and-legacy-driver"></a>Vista アプリケーションとレガシ ドライバーのマッピング


このセクションでは、Windows Vista アプリケーションを従来、ドライバーを使用する必要がある場合に使用されるマッピングを示します。 次の表では、従来の転送メッセージと転送の Windows Vista のメッセージへのデータ フローとデータ フローの WIA 互換性レイヤーのマップについて説明します。

### <a name="callback-transfers"></a>コールバックの転送

この表では、Windows Vista アプリケーションに送信されるメッセージを従来、ドライバーのコールバックの転送メッセージのマッピングを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>従来のドライバーの転送メッセージ</strong></p></td>
<td><p><strong>(互換性レイヤーの変換) した後、Windows Vista のアプリケーション メッセージ</strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p><strong>IStream::Seek、IStream::Write</strong>、および WIA_TRANSFER_MSG_STATUS すべて和です。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>無視されます。 このメッセージは、ドライバーではなく、サービスによってのみ送信され、この種類の転送中に送信しません。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>無視されます。 この種類の転送中に、このメッセージを受信しない必要があります。 従来、ドライバーは TYMED_CALLBACK または公開されていない TYMED_MULTIPAGE_CALLBACK を Windows Vista アプリケーションの複数ページ転送中にこれを送信してのみします。 互換レイヤーでは、TYMED_MULTIPAGE_FILE による複数ページの転送のみは。 TYMED_FILE 転送では、アプリケーションによって常に 1 つのページが一度に受信します。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>このメッセージは、ドライバーではなく、サービスによってのみ送信されます。 互換レイヤーは、代わりに WIA_TRANSFER_MSG_END_OF_STREAM および WIA_TRANSFER_MSG_END_OF_TRANSFER 送信されます。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>無視されます。 <strong>IStream</strong>転送モデルが帯域外のデータをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>無視されます。 <strong>IStream</strong>転送モデルが帯域外のデータをサポートしていません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>ファイル転送

この表では、Windows Vista アプリケーションに送信されるメッセージの従来のドライバーのファイル転送メッセージのマッピングを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>従来のドライバーの転送メッセージ</strong></p></td>
<td><p><strong>(互換性レイヤーの変換) した後、Windows Vista のアプリケーション メッセージ</strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p>無視されます。 ファイル転送中に、このメッセージを送信しない必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>無視されます。 このメッセージは、(ドライバー) ではなく、サービスによってのみ送信され、この種類の転送中に送信しません。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>無視されます。 この種類の転送中に、このメッセージを受信しない必要があります。 従来、ドライバーは TYMED_CALLBACK または公開されていない TYMED_MULTIPAGE_CALLBACK を Windows Vista アプリケーションの複数ページ転送中にこれを送信してのみします。 互換レイヤー、ただし、のみが TYMED_MULTIPAGE_FILE による複数ページ転送します。 TYMED_FILE 転送では、ドライバーによって常に 1 つのページが一度に受信します。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>このメッセージは、(ドライバー) ではなく、サービスによってのみ送信されます。 互換レイヤーは WIA_TRANSFER_MSG_END_OF_STREAM と WIA_TRANSFER_MSG_END_OF_TRANSFER 代わりに送信します。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>無視されます。 新しい転送モデルが帯域外のデータをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>無視されます。 新しい転送モデルが帯域外のデータをサポートしていません。</p></td>
</tr>
</tbody>
</table>

 

従来の転送メッセージの詳細については、次を参照してください。、 [IWiaMiniDrvCallBack インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)します。

TYMED 定数の詳細については、次を参照してください。[理解 TYMED](understanding-tymed.md)します。

**IStream**インターフェイスは、Microsoft Windows SDK ドキュメントで説明します。

 

 




