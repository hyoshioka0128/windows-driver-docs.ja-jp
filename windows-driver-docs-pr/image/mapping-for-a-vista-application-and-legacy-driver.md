---
title: Vista アプリケーションとレガシ ドライバーのマッピング
description: Vista アプリケーションとレガシ ドライバーのマッピング
ms.assetid: 176157b0-cc30-467b-95ec-2d25a40c43ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5030c378109caf03af950fc2aaf0ea148ad7053c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840785"
---
# <a name="mapping-for-a-vista-application-and-legacy-driver"></a>Vista アプリケーションとレガシ ドライバーのマッピング


このセクションでは、Windows Vista アプリケーションでレガシドライバーを使用する必要がある場合に使用するマッピングについて説明します。 次の表では、WIA 互換性レイヤーが従来の転送メッセージとデータフローを Windows Vista 転送メッセージとデータフローにマップする方法について説明します。

### <a name="callback-transfers"></a>コールバックの転送

次の表は、レガシドライバーのコールバックメッセージと、Windows Vista アプリケーションに送信されるメッセージとのマッピングを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>レガシドライバー転送メッセージ</strong></p></td>
<td><p><strong>Windows Vista アプリケーションメッセージ (互換性レイヤー変換後)</strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p><strong>Istream:: Seek、istream:: Write</strong>、および WIA_TRANSFER_MSG_STATUS はすべて連結されています。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>無効. このメッセージは、ドライバーによってではなく、サービスによってのみ送信され、この種類の転送中に送信されることはありません。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>無効. この種類の転送中にこのメッセージを受信することはできません。 レガシドライバーは、Windows Vista アプリケーションに公開されていない TYMED_CALLBACK または TYMED_MULTIPAGE_CALLBACK を使用した複数ページ転送中にのみこれを送信します。 互換性レイヤーでは、TYMED_MULTIPAGE_FILE を使用したマルチページ転送のみが行われます。 TYMED_FILE 転送の場合、アプリケーションは常に1ページずつ受信します。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>このメッセージは、ドライバーによってではなく、サービスによってのみ送信されます。 互換性レイヤーは、代わりに WIA_TRANSFER_MSG_END_OF_STREAM と WIA_TRANSFER_MSG_END_OF_TRANSFER を送信します。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>無効. <strong>IStream</strong>転送モデルは帯域外データをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>無効. <strong>IStream</strong>転送モデルは帯域外データをサポートしていません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="file-transfers"></a>ファイル転送

次の表は、レガシドライバーのファイル転送メッセージと、Windows Vista アプリケーションに送信されるメッセージとのマッピングを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>レガシドライバー転送メッセージ</strong></p></td>
<td><p><strong>Windows Vista アプリケーションメッセージ (互換性レイヤー変換後)</strong></p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA</p></td>
<td><p>無効. このメッセージは、ファイル転送中に送信することはできません。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_STATUS</p></td>
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_DATA_HEADER</p></td>
<td><p>無効. このメッセージは、(ドライバーではなく) サービスによってのみ送信され、この種類の転送中に送信されることはありません。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_NEW_PAGE</p></td>
<td><p>無効. この種類の転送中にこのメッセージを受信することはできません。 レガシドライバーは、Windows Vista アプリケーションに公開されていない TYMED_CALLBACK または TYMED_MULTIPAGE_CALLBACK を使用した複数ページ転送中にのみこれを送信します。 ただし、互換性レイヤーでは、TYMED_MULTIPAGE_FILE を使用した複数ページ転送のみが行われます。 TYMED_FILE 転送の場合、ドライバーは常に1ページずつ受信します。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_TERMINATION</p></td>
<td><p>このメッセージは、(ドライバーではなく) サービスによってのみ送信されます。 互換性レイヤーは、代わりに WIA_TRANSFER_MSG_END_OF_STREAM と WIA_TRANSFER_MSG_END_OF_TRANSFER を送信します。</p></td>
</tr>
<tr class="odd">
<td><p>IT_MSG_FILE_PREVIEW_DATA</p></td>
<td><p>無効. 新しい転送モデルでは、帯域外データはサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>IT_MSG_FILE_PREVIEW_DATA_HEADER</p></td>
<td><p>無効. 新しい転送モデルでは、帯域外データはサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

従来の転送メッセージの詳細については、「 [IWiaMiniDrvCallBack インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)」を参照してください。

TYMED 定数の詳細については、「 [TYMED](understanding-tymed.md)について」を参照してください。

**IStream**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

 

 




