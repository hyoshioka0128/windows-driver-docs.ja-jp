---
title: 著作権保護の実装
description: 著作権保護の実装
ms.assetid: 42d91ad3-615a-461a-846b-4876ac8decea
keywords:
- DVD デコーダー ミニドライバー WDK、著作権保護
- デコーダー ミニドライバー WDK DVD、著作権保護
- 著作権保護 WDK DVD デコーダー
- コンテンツのスクランブル システム WDK DVD デコーダー
- CSS の WDK DVD デコーダー
- DVD decrypters WDK
- キー交換 WDK DVD デコーダー
- WDK DVD デコーダーの復号化
- 暗号化の WDK DVD デコーダー
- 暗号化の WDK DVD デコーダー
- 認証の WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d352d4a10be9167c1216316029f285ee4936841c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374170"
---
# <a name="copyright-protection-implementation"></a>著作権保護の実装





Microsoft では (CSS) のスキームのスクランブル システム コンテンツに必要なソフトウェアを認証プロセスを容易にするため、DVD-ROM ドライブを認証し、DVD の復号化を使用してキーを転送することができます。 Microsoft は、DVD の復号化を付属していません。 代わりに、Microsoft は、ハードウェアまたはソフトウェアの decrypters 認証を許可するエージェントとして動作するオペレーティング システムのコードを提供します。

キーの交換プロセスが開始され、DVD のナビゲーター/スプリッター フィルターによって制御されます。 DVD デコーダーのミニドライバーは、次のセクションに示したプロパティを実装するだけです。 残りの部分は、その他のコンポーネントによって処理されます。

DVD の各入力ストリームでは、著作権保護のプロパティを受信します。 これは、DVD のすべてのストリームは、同じハードウェアによって制御される場合でも当てはまります。

ビデオ ポートのプロパティ セットの GUID は[KSPROPSETID\_CopyProt](https://msdn.microsoft.com/library/windows/hardware/ff566572)します。 使用可能なは、次のプロパティです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565140" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_CHLG_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565140)"><strong>KSPROPERTY_DVDCOPY_CHLG_KEY</strong></a></p></td>
<td><p>このプロパティでは、get と set の両方がサポートされています。 Get プロパティは、そのバス チャレンジのキーを提供するデコーダーを要求します。 プロパティの設定は、DVD ドライブから bus チャレンジのキーを使用して、デコーダーを提供します。 このプロパティで渡されるデータ型の構造体は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567636" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_CHLGKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567636)"> <strong>KS_DVDCOPY_CHLGKEY</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565145" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DVD_KEY1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565145)"><strong>KSPROPERTY_DVDCOPY_DVD_KEY1</strong></a></p></td>
<td><p>プロパティのセットのみです。 このプロパティは、デコーダーに DVD ドライブのバス キー 1 を提供します。 渡されたデータ型の構造体は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"> <strong>KS_DVDCOPY_BUSKEY</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565142" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DEC_KEY2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565142)"><strong>KSPROPERTY_DVDCOPY_DEC_KEY2</strong></a></p></td>
<td><p>取得専用プロパティです。 このプロパティは、デコーダーのバス キー 2 を DVD ドライブに転送を要求します。 渡されたデータ型の構造体は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"> <strong>KS_DVDCOPY_BUSKEY</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565148" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_TITLE_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565148)"><strong>KSPROPERTY_DVDCOPY_TITLE_KEY</strong></a></p></td>
<td><p>プロパティのセットのみです。 これは、現在のコンテンツからタイトル キーを提供します。 キーは、型の構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff567640" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567640)"> <strong>KS_DVDCOPY_TITLEKEY</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565144" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DISC_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565144)"><strong>KSPROPERTY_DVDCOPY_DISC_KEY</strong></a></p></td>
<td><p>プロパティのセットのみです。 これは、ディスクのキーを提供します。</p>
<div>
 
</div>
キーは、型の構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff567637" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567637)"> <strong>KS_DVDCOPY_DISCKEY</strong></a>します。</td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565114" data-raw-source="[&lt;strong&gt;KSPROPERTY_COPY_MACROVISION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565114)"><strong>KSPROPERTY_COPY_MACROVISION</strong></a></p></td>
<td><p>プロパティのセットのみです。 キーは、型の構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff567316" data-raw-source="[&lt;strong&gt;KS_COPY_MACROVISION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567316)"> <strong>KS_COPY_MACROVISION</strong></a>します。 これは、アナログ NTSC ビデオ ストリームであり、すぐに、NTSC macrovision プロパティを処理します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565146" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565146)"><strong>KSPROPERTY_DVDCOPY_REGION</strong></a></p></td>
<td><p>取得専用プロパティです。 DVD ミニドライバーは、正確に 1 つのリージョンのビットに適合します。 キーは、型の構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff567638" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567638)"> <strong>KS_DVDCOPY_REGION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565147" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565147)"><strong>KSPROPERTY_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
<td><p>プロパティの get および set のみです。 キーは、型の構造体<a href="https://msdn.microsoft.com/library/windows/hardware/ff567639" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567639)"> <strong>KS_DVDCOPY_SET_COPY_STATE</strong></a>します。 このプロパティを使用します。</p>
<p>KS_DVDCOPYSTATE_AUTHENTICATION_NOT_REQUIRED、</p>
<p>KS_DVDCOPYSTATE_AUTHENTICATION_REQUIRED、</p>
<p>KS_DVDCOPYSTATE_INITIALIZE と</p>
<p>KS_DVDCOPYSTATE_INITIALIZE_TITLE します。</p></td>
</tr>
</tbody>
</table>

 

次の順序は、デコーダーですべて開く DVD 入力ピンに繰り返されます。 デコーダーは、次の順序でキーを受け取ります。

取得 KSPROPERTY\_DVDCOPY\_CHLG\_キー

設定 KSPROPERTY\_DVDCOPY\_DVD\_[key1]

設定 KSPROPERTY\_DVDCOPY\_CHLG\_キー

取得 KSPROPERTY\_DVDCOPY\_DEC\_KEY2

設定 KSPROPERTY\_DVDCOPY\_ディスク\_キー

次に、次のキーが受信します。

取得 KSPROPERTY\_DVDCOPY\_CHLG\_キー

設定 KSPROPERTY\_DVDCOPY\_DVD\_[key1]

設定 KSPROPERTY\_DVDCOPY\_CHLG\_キー

取得 KSPROPERTY\_DVDCOPY\_DEC\_KEY2

設定 KSPROPERTY\_DVDCOPY\_タイトル\_キー

このシーケンスのものデコーダーですべて開く DVD 入力ピンで繰り返されます。 DVD ディスクのキーが正常に確立するには、ディスク キーごとに 1 回以上発生する可能性があります後にいつでも発生します。 タイトルのキーを含む、セクターが読み取られるたびに、認証プロセスを正常に完了する必要があります。 認証に失敗した場合は、読み取りはブロックされ、対応するエラー メッセージが返されます。

 

 




