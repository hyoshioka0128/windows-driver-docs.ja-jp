---
title: Microsoft OS 1.0 記述子の仕様
description: Microsoft OS 1.0 記述子の仕様
ms.assetid: A2B00584-DDD5-42D2-BDBF-116637ABD192
ms.date: 07/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 40f398f445d0b90f24347b36735cffd7603138e7
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210626"
---
# <a name="microsoft-os-10-descriptors-specification"></a>Microsoft OS 1.0 記述子の仕様


USB デバイスは、デバイスのファームウェアの標準記述子とそのインターフェイスとエンドポイントを格納します。 独立系ハードウェアベンダー (Ihv) は、クラスおよびベンダー固有の記述子を格納することもできます。 ただし、これらの記述子に含めることができる情報の種類は限られています。 通常、Ihv は、Windows Update または CD などのメディアを使用して、ユーザーに画像、アイコン、カスタムドライバーなどのさまざまなデバイス固有の情報を提供する必要があります。

この問題に対応するために、Microsoft では Microsoft OS 記述子を定義しています。 これらの記述子を使用すると、通常はユーザーに個別に提供される情報の多くをファームウェアに格納することができます。 Microsoft OS 記述子を認識している Windows のバージョンでは、制御要求を使用して情報を取得し、それを使用してユーザーの操作を必要とせずにデバイスをインストールおよび構成します。 このホワイトペーパーでは、Microsoft OS 記述子の概要について説明します。これには、それらがどのように保存および取得されるかについての説明が含まれます。

**注:**「拡張互換 ID OS 機能記述子の仕様」の付録1にある互換性のある Id と下位互換性のある Id の表は、仕様が書き込まれた時点で最新ですが、変更後の可能性があります。 次の表には、互換性のある Id と下位互換性のある Id の最新の一覧が含まれています。 すべての Id は8バイトである必要があるため、未使用の文字は Null で埋められます。

<table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<thead>
<tr align="left" valign="top">
<td>
<strong>互換 id</strong>
</td>
<td>
<strong>下位互換性 ID</strong>
</td>
<td>
<strong>説明</strong>
</td>
</tr>
</thead>
<tbody>
<tr align="left" valign="top">
<td>(0x00 0x00 0x00 0x00、0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00、0x00 0x00)</td>
<td>互換性のない ID または下位互換性のある ID</td>
</tr>
<tr align="left" valign="top">
<td>"RNDIS"<br>(0x52 0x4E 0x4e 0x4e 0x52 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00、0x00 0x00)</td>
<td>リモートネットワークドライバーインターフェイス標準 (RNDIS)</td>
</tr>
<tr align="left" valign="top">
<td>PTP<br>(0x50 0x54 0x50 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00、0x00 0x00)</td>
<td>画像転送プロトコル (PTP)</td>
</tr>
<tr align="left" valign="top">
<td>MTP<br>(0x4D 0x54 0x50 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00、0x00 0x00)</td>
<td>メディア転送プロトコル (MTP)</td>
</tr>
<tr align="left" valign="top">
<td>"XUSB20"<br>(0x58 0x55 0x58 0x42 0x32 0x30 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00、0x00 0x00)</td>
<td>XNACC (Krypton)</td>
</tr>
<tr align="left" valign="top">
<td>"BLUTUTH"<br>(0x42 0x4C 0x55 0x54 0x55 0x54 0x4c 0x00)</td>
<td>
<div class="contentTableWrapper"><table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<tbody>
<tr align="left" valign="top">
<td>個<br>(0x31 0x31 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>バージョン1.1 に準拠し、Microsoft ドライバースタックと互換性のある Bluetooth ラジオ</td>
</tr>
<tr align="left" valign="top">
<td>vdc<br>(0x31-0x32 0x00 0x00 0x00 0x00)</td>
<td>Microsoft ドライバースタックと互換性があり、バージョン1.2 に準拠している Bluetooth ラジオ</td>
</tr>
<tr align="left" valign="top">
<td>"EDR"<br>(0x45 0x45 0x52 0x00 0x00 0x00)</td>
<td>V2.0 + EDR に準拠し、Microsoft ドライバースタックと互換性のある Bluetooth ラジオ</td>
</tr>
</tbody>
</table></div>
<p>
<br>
</p>
</td>
<td>[Bluetooth]</td>
</tr>
<tr align="left" valign="top">
<td>取り込む<br>(0x53 0x43 0x43 0X43 0x00 0x00 0x00)</td>
<td>
<p>形式は次のとおりです: 2 文字ベンダーコード + 1-5 ASCII 文字 * + 0x00</p>
<p>* ASCII 文字を大文字、数字、アンダースコアに制限します。</p>
</td>
<td>Scan</td>
</tr>
<tr align="left" valign="top">
<td>"3DPRINT"<br>(0x33 0x44 0x50 0x52 0x44 0X44 0x52 0x00)</td>
<td>不定</td>
<td>MS3DPRINT G-Code 3D プリンター</td>
</tr>
</tbody>
</table>

  

この情報は、windows XP 以降のバージョンの Windows に適用されます。

**続行する前に、使用許諾契約書をお読みください。**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td style="text-align: center;"><strong><br />
Microsoft OS 記述子の仕様</strong><br />
</td>
</tr>
<tr class="even">
<td style="text-align: center;"><div style="font-size: 100%; border: thin inset; height: 400px; overflow: scroll; text-align: left; padding: 10px;">
<h3 id="microsoft-os-descriptor-specification-license-agreement">Microsoft OS 記述子仕様の使用許諾契約書</h3>
<p>この仕様については、お客様 (個人または単一のエンティティ) と Microsoft Corporation ("Microsoft") の間の法的契約 ("契約") です。仕様をダウンロード、コピー、またはその他の方法で使用することにより、本ライセンス条項に従うことに同意したことになります。   </p>
<p><strong>セクション1の定義。</strong></p>
<p>(a) "お客様の実装" とは、「Microsoft OS 記述子が有効になっているオペレーティングシステムとのインターフェイスの仕様」で説明されている OS 記述子セットを実装する (i) ファームウェアやハードウェア、またはこの情報を取得して使用するために Microsoft が承認しているその他のシステムを意味します。および (ii) Windows Vista または Windows 7 オペレーティングシステムとのインターフェイスのみを対象として、仕様に記述されている OS 記述子セットを実装するソフトウェアドライバー。</p>
<p>(b) "your ライセンス" は、お客様の実装を使用するためにお客様によってライセンスされるサードパーティを意味します。</p>
<p>(c) "仕様" は、Microsoft の OS 記述子仕様と付随する資料を意味します。</p>
<p><strong>セクション2ライセンスの付与</strong>。</p>
<p>ある    <strong>著作権ライセンス</strong>。Microsoft は、仕様におけるマイクロソフトの著作権、非揮発性、ロイヤリティフリー、nontransferable、マイクロソフト以外の個人所有者による仕様のコピーを社内で自動的に再現することをお客様に許諾します。実装の開発には、契約者が使用します。</p>
<p>b   <strong>特許ライセンス</strong>。Microsoft は、仕様内のみに含まれており、microsoft によって所有またはライセンス対象されているマイクロソフトの特許に基づいて、お客様に対して非限定、ロイヤリティフリーの nontransferable、世界中のライセンスをお客様に許可します。実装のライセンスに直接または間接的に配布します。この特許ライセンスは、ライセンスに同じ使用条件でサブライセンスを付与することができます。</p>
<p>40u-c    <strong>権利の予約</strong>。Microsoft は、仕様、実装、およびその他の知的財産に含まれるその他のすべての権利を留保します。このドキュメントは、その他のマイクロソフトの特許、商標、著作権、またはその他の無体財産権に関するいかなる団体にも付与されません。 </p>
<p><strong>セクション3の制限事項と義務について説明</strong>します。</p>
<p>(a) 仕様に対するライセンスの権利は、ライセンスされた実装を作成、変更、または配布することができないように規定されています。このような場合は、作成、変更、または配布する場合があります。仕様 (またはその中の知的財産) または (b) 権利に対して、任意のサードパーティに対して任意の権利を付与するか、または仕様の中で所有権を immunities します。</p>
<p>(b) この契約の使用条件に準拠していない場合、マイクロソフトは、他の権利を風ことなく、本契約を終了することがあります。 このようなイベントでは、仕様のすべてのコピーを破棄する必要があり、それ以上会社の実装を配布することはできません。</p>
<p><strong>セクション4保証の免責事項。</strong></p>
<p>仕様は、いかなる種類の保証も伴わず、「現状有姿」で提供されます。 Microsoft は、適用法によって許可される最大範囲に対して、商品性や特定目的への適合性に関する黙示の保証や、権原と第三者を保証することを除いて、いかなる保証も一切いたしません。 仕様の使用やパフォーマンスに起因するリスク全体は、お客様の責任を負うものとします。</p>
<p><strong>セクション5では、付随的、派生的、およびその他の損害の除外について説明します。</strong></p>
<p><strong>適用法によって許容される最大の範囲において、マイクロソフトまたはそのサプライヤーは一切の責任を負わないものとします。このような損害の可能性が Microsoft によって認められている場合でも、付随的、直接的、間接、特殊、懲罰的損害、またはその他の損害 (制限なく、ビジネスの利益の損失、ビジネスの中断、ビジネス情報の損失、ビジネス情報の損失、業務情報の損失、その他の pecuniary 損失など) が発生します。一部の州/管轄区域では、派生または付随的損害に対する責任の除外または制限が認められないため、上記の制限は適用されない場合があります。</strong></p>
<p><strong>セクション 6. 責任および救済手段の制限。</strong></p>
<p><strong>何らかの理由で発生する可能性のある損害 (ただし、上記のすべての損害と、直接的または一般的な損害を含む) については、マイクロソフトとそのサプライヤーのすべての責任は、本契約と、上記のすべてを対象とした排他的な救済手段は、この仕様に対して実際に支払った金額、または米国 $ 5.00 に限定されるものとします。前述の制限事項、除外事項、免責事項は、適用法によって許容される最大範囲に適用されるものとします</strong></p>
<p><strong>セクション7準拠法</strong>。</p>
<p>この仕様を米国で取得した場合、本契約はワシントン州の法律に準拠するものとします。 本契約が発生する可能性がある争議に関しては、ワシントン州キング郡にある州と連邦裁判所の管轄に同意したことになります。</p>
<p><strong>セクション8の割り当て。</strong></p>
<p>第三者に事前に書面による承認を受けることなく、この契約を割り当てることはできません。</p>
</div>
<p><br />
<a href="https://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/OS_Desc_Ext_Prop.zip">同意してダウンロード</a></p></td>
</tr>
</tbody>
</table>