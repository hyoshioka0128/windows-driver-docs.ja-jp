---
Description: オブジェクトの要件
title: オブジェクトの要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e82b7ac5ea59f790083e9331fc3f335fe007c00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385401"
---
# <a name="requirements-for-objects"></a>オブジェクトの要件


Windows ポータブル デバイス (WPD) は、コンテンツの種類からのすべてのオブジェクトを分類します。 特定の型のオブジェクトが最小の一覧のプロパティやリソース (および、デバイス オブジェクト、一連のコマンド) をサポートするために必要です。 オブジェクトの型はその[WPD\_オブジェクト\_コンテンツ\_型](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597893(v=vs.85)#wpd-object-content-type)プロパティはすべてのオブジェクトは、このプロパティをサポートする必要があります。

WPD は、(GUID 値) として、次のコンテンツ タイプを定義します。 仕入先は、独自の GUID を提供することで、独自のカスタム コンテンツ タイプを作成できます。

注の一般的な用途に利用通常 1 つしか処理の定義済みの型。 ベンダーのアプリケーションには、認識していること、カスタムの型の完全な利用します。

各オブジェクトの種類をサポートする必要がありますプロパティおよびリソースについては、次の表に、オブジェクトの種類ごとの説明 ページを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンテンツの種類の GUID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597834(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_ALL&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597834(v=vs.85))"><strong>WPD_CONTENT_TYPE_ALL</strong></a></td>
<td align="left">このコンテンツの種類によってすべてのデバイス タイプに興味のあることを示す特定のクエリ メソッドを使用してのみです。この型のオブジェクトを作成することはできません。
<p>カスタム オブジェクトを設計する場合は、少なくとも、これらのプロパティをサポートしてする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597835(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_APPOINTMENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597835(v=vs.85))"><strong>WPD_CONTENT_TYPE_APPOINTMENT</strong></a></td>
<td align="left">オブジェクトには、カレンダーの予定です。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597836(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_AUDIO&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597836(v=vs.85))"><strong>WPD_CONTENT_TYPE_AUDIO</strong></a></td>
<td align="left">オブジェクトは、オーディオ ファイル、WMA または MP3 ファイルなどです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597837(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_AUDIO_ALBUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597837(v=vs.85))"><strong>WPD_CONTENT_TYPE_AUDIO_ALBUM</strong></a></td>
<td align="left">オブジェクトは、オーディオ、アルバムです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597838(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CALENDAR&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597838(v=vs.85))"><strong>WPD_CONTENT_TYPE_CALENDAR</strong></a></td>
<td align="left">オブジェクトは、カレンダーです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597839(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CERTIFICATE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597839(v=vs.85))"><strong>WPD_CONTENT_TYPE_CERTIFICATE</strong></a></td>
<td align="left">オブジェクトは、認証に使用される証明書です。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597840(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CONTACT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597840(v=vs.85))"><strong>WPD_CONTENT_TYPE_CONTACT</strong></a></td>
<td align="left">オブジェクトは、個人の連絡先データを vCard ファイルです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597841(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_CONTACT_GROUP&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597841(v=vs.85))"><strong>WPD_CONTENT_TYPE_CONTACT_GROUP</strong></a></td>
<td align="left">オブジェクトは、連絡先のグループを表します。 このオブジェクトの WPD_OBJECT_REFERENCES プロパティには、各種 WPD_CONTENT_TYPE_CONTACT オブジェクトのオブジェクト識別子の一覧が含まれています。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597842(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_DOCUMENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597842(v=vs.85))"><strong>WPD_CONTENT_TYPE_DOCUMENT</strong></a></td>
<td align="left">オブジェクトは、テキスト、書式設定の有無のコンテナーです。 例には、Microsoft Word ファイルやプレーン テキスト ファイルが含まれます。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597843(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_EMAIL&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597843(v=vs.85))"><strong>WPD_CONTENT_TYPE_EMAIL</strong></a></td>
<td align="left">オブジェクトは、電子メール メッセージです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597844(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_FOLDER&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597844(v=vs.85))"><strong>WPD_CONTENT_TYPE_FOLDER</strong></a></td>
<td align="left">オブジェクトは、フォルダーです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597845(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597845(v=vs.85))"><strong>WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT</strong></a></td>
<td align="left">オブジェクトは、デバイスの機能を表す機能オブジェクトです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597846(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_GENERIC_FILE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597846(v=vs.85))"><strong>WPD_CONTENT_TYPE_GENERIC_FILE</strong></a></td>
<td align="left">オブジェクトは、ファイルの他の定義済みのコンテンツ タイプのいずれにも該当しない汎用の物理ファイルです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597848(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_IMAGE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597848(v=vs.85))"><strong>WPD_CONTENT_TYPE_IMAGE</strong></a></td>
<td align="left">オブジェクトは、JPEG ファイルなどの静止画です。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597849(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_IMAGE_ALBUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597849(v=vs.85))"><strong>WPD_CONTENT_TYPE_IMAGE_ALBUM</strong></a></td>
<td align="left">オブジェクトは、イメージのアルバムです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597851(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MEDIA_CAST&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597851(v=vs.85))"><strong>WPD_CONTENT_TYPE_MEDIA_CAST</strong></a></td>
<td align="left">オブジェクトは、キャスト メディア オブジェクトです。 キャスト メディア オブジェクトは、グループがオンラインで公開されているコンテンツを関連コンテナー オブジェクトを表すことができます。 たとえば、RSS チャネルは、キャスト メディア オブジェクトとして表現できるし、WPD_OBJECT_REFERENCES プロパティこのオブジェクトのにはチャネル内の各項目を表すオブジェクト識別子の一覧が含まれています。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597851(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MEMO&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597851(v=vs.85))"><strong>WPD_CONTENT_TYPE_MEMO</strong></a></td>
<td align="left">オブジェクトは、テキスト メモたとえば、メモ型のデータを表します。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597852(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_MIXED_CONTENT_ALBUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597852(v=vs.85))"><strong>WPD_CONTENT_TYPE_MIXED_CONTENT_ALBUM</strong></a></td>
<td align="left">オブジェクトが混合メディア オブジェクトのアルバム、オーディオ、画像、およびビデオ ファイルなどです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597854(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_PLAYLIST&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597854(v=vs.85))"><strong>WPD_CONTENT_TYPE_PLAYLIST</strong></a></td>
<td align="left">オブジェクトは、再生リストです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597855(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_PROGRAM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597855(v=vs.85))"><strong>WPD_CONTENT_TYPE_PROGRAM</strong></a></td>
<td align="left">オブジェクトは、実行できる、たとえば、スクリプトまたは実行可能ファイルを表します。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597856(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_SECTION&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597856(v=vs.85))"><strong>WPD_CONTENT_TYPE_SECTION</strong></a></td>
<td align="left">オブジェクトには、別のオブジェクトに含まれるデータのセクションについて説明します。 など、大規模なオーディオ ファイルは、一連の章の最適な説明可能性があります。 各章には、独自の章のアート、メタデータ、および、使用して、WPD_CONTENT_TYPE_SECTION オブジェクト可能性があり、データが含まれる大規模なオーディオ ファイルのサブセット (たとえば、最初の章では、最初の 10 分、2 番目の章では、次の 20 分、など)。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597857(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_TASK&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597857(v=vs.85))"><strong>WPD_CONTENT_TYPE_TASK</strong></a></td>
<td align="left">オブジェクトは、to do リスト内の項目などのタスクです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597858(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_TELEVISION&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597858(v=vs.85))"><strong>WPD_CONTENT_TYPE_TELEVISION</strong></a></td>
<td align="left">オブジェクトでは、テレビの録画です。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597859(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_UNSPECIFIED&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597859(v=vs.85))"><strong>WPD_CONTENT_TYPE_UNSPECIFIED</strong></a></td>
<td align="left">オブジェクトは、定義済みの WPD コンテンツの種類にも該当しない汎用オブジェクトです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597860(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_VIDEO&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597860(v=vs.85))"><strong>WPD_CONTENT_TYPE_VIDEO</strong></a></td>
<td align="left">オブジェクトは、WMV AVI ファイルなどのビデオです。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597861(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_VIDEO_ALBUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597861(v=vs.85))"><strong>WPD_CONTENT_TYPE_VIDEO_ALBUM</strong></a></td>
<td align="left">オブジェクトは、アルバムのビデオです。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597862(v=vs.85)" data-raw-source="[&lt;strong&gt;WPD_CONTENT_TYPE_WIRELESS_PROFILE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597862(v=vs.85))"><strong>WPD_CONTENT_TYPE_WIRELESS_PROFILE</strong></a></td>
<td align="left">オブジェクトには、ワイヤレス ネットワークへのアクセスの情報が含まれています。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597563(v=vs.85)" data-raw-source="[Device Object](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597563(v=vs.85))">デバイス オブジェクト</a></td>
<td align="left">ありません、 <strong>PROPERTYKEY</strong>が、すべてのオブジェクトがこのセクションに示したプロパティをサポートする必要があります。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





