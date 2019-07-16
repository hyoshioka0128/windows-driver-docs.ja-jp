---
title: Microsoft OS 1.0 記述子の仕様
description: Microsoft OS 1.0 記述子の仕様
ms.assetid: A2B00584-DDD5-42D2-BDBF-116637ABD192
ms.date: 07/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 10dbb8cc465684b78adb90c37c7090e97599bf1b
ms.sourcegitcommit: 707739250ebdcd74a26d85d8b4217fa81c9c9e95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68181287"
---
# <a name="microsoft-os-10-descriptors-specification"></a>Microsoft OS 1.0 記述子の仕様


USB デバイスは、デバイス、インターフェイス、およびエンドポイントのファームウェアに標準の記述子を格納します。 また、独立系ハードウェア ベンダー (Ihv) は、クラスとベンダー固有の記述子を格納していることもできます。 ただし、これらの記述子を格納できる情報の種類が制限されています。 Ihv 通常必要がありますを使用して、Windows Update または CD などのメディアなど、ユーザーにさまざまな画像、アイコン、カスタム ドライバーなどのデバイスに固有の情報を提供します。

Ihv はこの問題に対処するために、Microsoft が Microsoft OS ディスクリプターを定義します。 これらの記述子は、ファームウェアではこれで通常お客様に個別に提供情報の多く格納する Ihv で使用できます。 バージョンの Microsoft OS ディスクリプターを認識している Windows のコントロールの要求を使用して、情報を取得して、インストールして、ユーザーの介入を必要とせずにデバイスを構成します。 このホワイト ペーパーでは、Microsoft OS ディスクリプターを格納および取得の方法の説明などを紹介します。

**注:** 「拡張互換性 ID OS 機能記述子の仕様」の付録 1 での互換性と下位互換性のある Id のテーブルは現在時点仕様が書き込まれましたが、ため変更可能性があります。 次の表には、最新の互換性と下位互換性のある Id の一覧が含まれています。 すべての Id は、使用されていない文字が Null で埋められますので、8 バイトにすることがあります。

<table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<thead>
<tr align="left" valign="top">
<td>
<strong>CompatibleID</strong>
</td>
<td>
<strong>下位互換性のある ID</strong>
</td>
<td>
<strong>説明</strong>
</td>
</tr>
</thead>
<tbody>
<tr align="left" valign="top">
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>互換性または下位互換性のある ID がありません。</td>
</tr>
<tr align="left" valign="top">
<td>"RNDIS"<br>(0x52 0x4E 0x44 0x49 0x53 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>リモート ネットワーク ドライバー インターフェイスの標準 (RNDIS)</td>
</tr>
<tr align="left" valign="top">
<td>"PTP"<br>(0x50 0x54 0x50 0x00 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>画像転送プロトコル (PTP)</td>
</tr>
<tr align="left" valign="top">
<td>"MTP"<br>(0x4D 0x54 0x50 0x00 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>メディア転送プロトコル (MTP)</td>
</tr>
<tr align="left" valign="top">
<td>"XUSB20"<br>(0x58 0x55 0x53 0x42 0x32 0x30 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>XNACC (Krypton)</td>
</tr>
<tr align="left" valign="top">
<td>"BLUTUTH"<br>(0x42 0x4C 0x55 0x54 0x55 0x54 0x48 0x00)</td>
<td>
<div class="contentTableWrapper"><table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<tbody>
<tr align="left" valign="top">
<td>「11」<br>(0x31 0x31 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>Bluetooth 無線 v1.1 に準拠し、Microsoft ドライバー スタックとの互換性</td>
</tr>
<tr align="left" valign="top">
<td>「12」<br>(0x31 0x32 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>Bluetooth 無線 v1.2 に準拠し、Microsoft ドライバー スタックとの互換性</td>
</tr>
<tr align="left" valign="top">
<td>"EDR"<br>(0x45 0x44 0x52 0x00 0x00 0x00 0x00 0x00)</td>
<td>Bluetooth 無線 v2.0 + EDR に準拠し、Microsoft ドライバー スタックとの互換性</td>
</tr>
</tbody>
</table></div>
<p>
<br>
</p>
</td>
<td>Bluetooth</td>
</tr>
<tr align="left" valign="top">
<td>「スキャン」<br>(0x53 0x43 0x41 0x4E 0x00 0x00 0x00 0x00)</td>
<td>
<p>次のように書式設定します。2 文字のベンダー コード + 1 ~ 5 の ASCII 文字 * + 0x00</p>
<p>\* ASCII は、大文字、数字、アンダー スコアに制限します。</p>
</td>
<td>Scan</td>
</tr>
<tr align="left" valign="top">
<td>"3DPRINT"<br>(0x33 0x44 0x50 0x52 0x49 0x4E 0x54 0x00)</td>
<td>不定</td>
<td>MS3DPRINT G コードの 3D プリンター</td>
</tr>
</tbody>
</table>

  

この情報は、Windows XP および Windows の以降のバージョンに適用されます。

**続行する前にライセンス契約をお読みください。**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td style="text-align: center;"><strong><br />
Microsoft OS ディスクリプター仕様</strong><br />
</td>
</tr>
<tr class="even">
<td style="text-align: center;"><div style="font-size: 100%; border: thin inset; height: 400px; overflow: scroll; text-align: left; padding: 10px;">
<h3 id="microsoft-os-descriptor-specification-license-agreement">Microsoft OS ディスクリプター仕様許諾契約書</h3>
<p>これは、(どちらを単独、または 1 つのエンティティ) のお客様との間の法的契約 (「契約」) ("You")、および Microsoft Corporation ("Microsoft") の仕様。  ダウンロード、コピー、またはそれ以外の場合、仕様を使用して、によって、本契約の条項に拘束されることに同意したことにします。   </p>
<p><strong>セクション 1 定義します。</strong></p>
<p>(a)「の実装」の意味、: (i) ファームウェアや、Microsoft OS ディスクリプターを有効になっているオペレーティング システムとのインターフェイスの仕様に記載されている OS 記述子セットを取得するために Microsoft によって承認されたその他のシステムを実装するハードウェアとこの情報を使用して、OS の記述子の実装設定を (ii) ソフトウェア ドライバーが Windows Vista または Windows 7 と組み合わせた場合にのみインターフェイス仕様でオペレーティング システムを説明します。</p>
<p>(b)「のライセンシー」は、サード パーティが、実装を使用することによってライセンス供与を意味します。</p>
<p>(c)「仕様」は、Microsoft の OS の記述子の仕様と付随するマテリアルを意味します。</p>
<p><strong>セクション 2 は、ライセンスの付与</strong>します。</p>
<p>(a)    <strong>著作権ライセンス</strong>します。  マイクロソフトは許諾、仕様では、Microsoft の著作権の下で、非独占的なロイヤリティ フリー、譲渡、ことのできない世界する個人ライセンスを内部的には、仕様のコピーを作成し、請負業者の Your 実装を開発します。</p>
<p>(b)   <strong>特許ライセンス</strong>します。  Microsoft をここに許諾するマイクロソフトの特許の仕様の中にのみ、非独占的、無償、譲渡、世界中のライセンスとことを使用して、インポート、販売、販売を提供する Microsoft によって所有されているか、ライセンスにあるとライセンスの実装に直接または間接的を配布します。  同じ条項および条件下で、ライセンスをこの特許ライセンス者にサブライセンスする可能性があります。</p>
<p>(c)    <strong>権利の留保</strong>します。  マイクロソフトでは、本仕様では、その実装および知的財産必要がありますすべての権利を留保します。  このドキュメントへは与えられませんするか、他のエンティティのライセンス、その他のマイクロソフトの特許、商標、著作権、またはその他の知的財産権。 </p>
<p><strong>セクション 3 追加の制限事項と義務</strong>します。</p>
<p>(仕様に権利が条件を作成するので、変更、またはこのような作成、変更、または配布可能性のある方法で、ライセンスの実装を配布する (a) となりますが、a)、ライセンスの作成、または Microsoft の遵守義務を作成するよう主張仕様は (または知的財産権その) または (b) grant、または与えるには、第三者に権限またはマイクロソフトの知的財産や財産権の仕様を immunities purport します。</p>
<p>(b) その他の権限を損なう、本契約の条件に準拠するために失敗した場合、Microsoft は本契約を終了する可能性があります。 このようなイベントでは、仕様のすべてのコピーを破棄する必要があり、会社の実装をさらに配布する必要があります。</p>
<p><strong>セクション 4 あらゆる保証の免責。</strong></p>
<p>仕様は、いかなる保証も伴わず"IS"として提供されます。 適用される法令により認められる限り、さらに、Microsoft は一切の保証はありません、制限なしを含む、暗黙の商品性および特定目的に対する適合性の保証と title および非侵害の保証します。 すべての使用または仕様の性能によって生じるリスクなります。</p>
<p><strong>セクション 5 除外派生的損害、付随的損害です。</strong></p>
<p><strong>適用される法令により認められる限り、いかなる場合においてマイクロソフトまたはそのサプライヤー負いませんその派生的損害、付随的損害、直接、間接、特別な懲罰、またはその他の損害一切を含め、制限、損害の損失を防ぐ業務利益、業務の中断、業務の情報の損失または他の金銭損失) Microsoft がこのような損害の可能性について知らされていた場合でも、仕様を使用すること、または使用から発生しました。派生的損害または付随的損害に対する賠償責任の制限または除外事項、一部の地域が認められないため、上記の制限がするには適用されません。</strong></p>
<p><strong>責任のセクション 6 制限します。</strong></p>
<p><strong>上記で低下することが理由の如何に関わらずを含め、制限、上記すべての損害、およびすべての直接または一般的な損害)、マイクロソフトおよびその供給者のこの規定のいずれかのいずれかの責任アグリーメントとお客様独自の救済前述のすべては、大きいに限定されるものと仕様または U.S.$5.00 が実際に支払った金額の。上記の制限事項、除外および免責事項は、あらゆる救済手段には、本質的な目的が失敗した場合でも、法律で許可される最大の範囲に適用されるものです。</strong></p>
<p><strong>SECTION 7 準拠法</strong>します。</p>
<p>米国の州には、この仕様を取得する場合は、本契約はワシントン州の法律によって制御されます。 本契約の履行に発生する可能性争議、状態と、ワシントン州キング郡の連邦裁判所の管轄区域に同意したことにします。</p>
<p><strong>セクション 8 の割り当て。</strong></p>
<p>どちらの当事者も割り当てることがこの契約書承認他方の当事者の書面します。</p>
</div>
<p><br />
<a href="http://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/OS_Desc_Ext_Prop.zip">ダウンロードに同意</a></p></td>
</tr>
</tbody>
</table>