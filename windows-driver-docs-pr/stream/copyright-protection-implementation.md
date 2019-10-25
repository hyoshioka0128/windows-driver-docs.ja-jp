---
title: 著作権保護の実装
description: 著作権保護の実装
ms.assetid: 42d91ad3-615a-461a-846b-4876ac8decea
keywords:
- DVD デコーダーミニドライバー WDK、著作権保護
- デコーダーミニドライバー WDK DVD、著作権保護
- 著作権保護 WDK DVD デコーダー
- コンテンツスクランブルシステム WDK DVD デコーダー
- CSS WDK DVD デコーダー
- DVD decrypters WDK
- キー交換 WDK DVD デコーダー
- 暗号化解除 WDK DVD デコーダー
- 暗号化 WDK DVD デコーダー
- 暗号化 WDK DVD デコーダー
- 認証 WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40301eaf946f6306bca2f0911b4204a8708f44b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844703"
---
# <a name="copyright-protection-implementation"></a>著作権保護の実装





Microsoft では、コンテンツスクランブルシステム (CSS) スキームによって要求される認証プロセスを容易にするソフトウェアを提供しています。これにより、dvd-rom ドライブは、DVD decrypter を使用してキーを認証および転送できます。 Microsoft は、DVD decrypter を出荷していません。 代わりに、Microsoft では、ハードウェアまたはソフトウェアの decrypters の認証を許可するために、エージェントとして機能するオペレーティングシステムのコードを提供しています。

キー交換プロセスは、DVD ナビゲーター/スプリッターフィルターによって開始および制御されます。 DVD デコーダーミニドライバーは、次のセクションに記載されているプロパティのみを実装する必要があります。 残りは、他のコンポーネントによって処理されます。

各 DVD 入力ストリームは、著作権保護のプロパティを受け取ります。 これは、すべての DVD ストリームが同じハードウェアによって制御されている場合でも当てはまります。

ビデオポートのプロパティセットの GUID は、 [Ksk Propsetid\_CopyProt](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-copyprot)です。 次のプロパティを使用できます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-chlg-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_CHLG_KEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-chlg-key)"><strong>KSPROPERTY_DVDCOPY_CHLG_KEY</strong></a></p></td>
<td><p>このプロパティでは、get と set の両方がサポートされています。 Get プロパティは、デコーダーにバスチャレンジキーを提供するよう要求します。 Set プロパティは、DVD ドライブからのバスチャレンジキーをデコーダーに提供します。 このプロパティで渡されるデータは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_chlgkey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_CHLGKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_chlgkey)"><strong>KS_DVDCOPY_CHLGKEY</strong></a>型の構造体です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dvd-key1" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DVD_KEY1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dvd-key1)"><strong>KSPROPERTY_DVDCOPY_DVD_KEY1</strong></a></p></td>
<td><p>設定専用のプロパティ。 このプロパティは、DVD ドライブバスキー1をデコーダーに提供します。 渡されるデータは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a>型の構造体です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dec-key2" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DEC_KEY2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dec-key2)"><strong>KSPROPERTY_DVDCOPY_DEC_KEY2</strong></a></p></td>
<td><p>取得専用のプロパティ。 このプロパティは、デコーダーのバスキー2を DVD ドライブに転送するように要求します。 渡されるデータは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_buskey)"><strong>KS_DVDCOPY_BUSKEY</strong></a>型の構造体です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-title-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_TITLE_KEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-title-key)"><strong>KSPROPERTY_DVDCOPY_TITLE_KEY</strong></a></p></td>
<td><p>設定専用のプロパティ。 これにより、現在のコンテンツからのタイトルキーが提供されます。 キーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_titlekey)"><strong>KS_DVDCOPY_TITLEKEY</strong></a>型の構造体です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-disc-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DISC_KEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-disc-key)"><strong>KSPROPERTY_DVDCOPY_DISC_KEY</strong></a></p></td>
<td><p>設定専用のプロパティ。 これにより、ディスクキーが提供されます。</p>
<div>
 
</div>
キーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_disckey)"><strong>KS_DVDCOPY_DISCKEY</strong></a>型の構造体です。</td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-copy-macrovision" data-raw-source="[&lt;strong&gt;KSPROPERTY_COPY_MACROVISION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-copy-macrovision)"><strong>KSPROPERTY_COPY_MACROVISION</strong></a></p></td>
<td><p>設定専用のプロパティ。 キーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision" data-raw-source="[&lt;strong&gt;KS_COPY_MACROVISION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)"><strong>KS_COPY_MACROVISION</strong></a>型の構造体です。 これはアナログ NTSC ビデオストリームで、間もなく NTSC macrovision プロパティを処理します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-region" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_REGION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-region)"><strong>KSPROPERTY_DVDCOPY_REGION</strong></a></p></td>
<td><p>取得専用のプロパティ。 DVD ミニドライバーは、1つのリージョンビットにのみ適合します。 キーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_region" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_REGION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_region)"><strong>KS_DVDCOPY_REGION</strong></a>型の構造体です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-set-copy-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-set-copy-state)"><strong>KSPROPERTY_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
<td><p>Get および set 専用のプロパティ。 キーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)"><strong>KS_DVDCOPY_SET_COPY_STATE</strong></a>型の構造体です。 このプロパティはを使用します。</p>
<p>KS_DVDCOPYSTATE_AUTHENTICATION_NOT_REQUIRED,</p>
<p>KS_DVDCOPYSTATE_AUTHENTICATION_REQUIRED,</p>
<p>KS_DVDCOPYSTATE_INITIALIZE、</p>
<p>KS_DVDCOPYSTATE_INITIALIZE_TITLE.</p></td>
</tr>
</tbody>
</table>

 

次のシーケンスは、デコーダーのすべての開いている DVD 入力ピンで繰り返されます。 デコーダーは、次の順序でキーを受け取ります。

DVDCOPY\_CHLG\_キー\_KSK プロパティを取得します。

KSK プロパティ\_DVDCOPY\_DVD\_KEY1 に設定します

DVDCOPY\_CHLG\_キー\_の KSK プロパティの設定

DVDCOPY\_DEC\_KEY2 に\_KSK プロパティを取得します。

DVDCOPY\_ディスク\_キー\_の KSK プロパティの設定

次に、次のキーを受け取ります。

DVDCOPY\_CHLG\_キー\_KSK プロパティを取得します。

KSK プロパティ\_DVDCOPY\_DVD\_KEY1 に設定します

DVDCOPY\_CHLG\_キー\_の KSK プロパティの設定

DVDCOPY\_DEC\_KEY2 に\_KSK プロパティを取得します。

DVDCOPY\_TITLE\_キーの\_の設定 KSK プロパティ

このシーケンスは、デコーダーで開いているすべての DVD 入力ピンにも繰り返し使用されます。 DVD ディスクキーが正常に確立され、ディスクキーごとに複数回発生する可能性があります。 タイトルキーを含むセクターが読み取られるたびに、認証プロセスが正常に完了している必要があります。 認証が失敗した場合、読み取りはブロックされ、対応するエラーメッセージが返されます。

 

 




