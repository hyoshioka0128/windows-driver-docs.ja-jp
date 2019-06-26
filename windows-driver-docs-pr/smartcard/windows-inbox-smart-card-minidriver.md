---
title: Windows Inbox スマート カード ミニドライバー
description: Windows Inbox スマート カード ミニドライバー
ms.assetid: 4B61607E-090A-4935-B944-110ACE9A4D83
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e80abba0d39b8dc0e61905f647d11b17af8f08f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369591"
---
# <a name="windows-inbox-smart-card-minidriver"></a>Windows Inbox スマート カード ミニドライバー


Windows 7 Service Pack 1 (SP1) 以降では、受信トレイのジェネリック クラス ミニドライバー PIV 準拠のスマート カードと GID カードの端を実装するカードをサポートする提供です。

PIV 準拠のスマート カードとカード、GID を実装するカードのエッジ。 PIV の詳細については、次を参照してください。、[について Personal Identity Verification (PIV) の連邦政府の官吏および請負業者](http://csrc.nist.gov/groups/SNS/piv/index.mdl)web ページ。

GID の詳細については、次を参照してください。、[ジェネリック Identity Device Specification](https://msdn.microsoft.com/windows/hardware/gg487496) web ページ。

スマート カードをリーダーと Base CSP または KSP に挿入するときに呼び出す[ **CardAcquireContext**](https://docs.microsoft.com/previous-versions/dn468701(v=vs.85))、クラス ミニドライバー PIV-いずれかとして関連付けられているカードをマークする次の検出プロセスを実行しますかGID に準拠していません。

1.  SELECT コマンドが発行すると、PIV AID を見つけます。 Windows が、PIV するカードを考慮して、コマンドが成功すると、デバイスと、検出処理が終了します。
2.  コマンドが失敗した場合、SELECT コマンドは、GID AID を検索に発行されます。 Windows が、GID デバイスと、検出するカードを考慮して、コマンドが成功すると、処理が終了します。
3.  コマンドは、どちらの補助がスマート カード上に存在するかを示すステータス コードで失敗した場合、Windows でも、カード、GID デバイスの場合とが処理されます。 コマンドは、その他のエラーで失敗した場合、Windows はカードを使用すると、不明なデバイスであると見なします。

## <a name="span-idelectricalprofileforgidscardswiththemicrosoftgenericprofilespanspan-idelectricalprofileforgidscardswiththemicrosoftgenericprofilespanspan-idelectricalprofileforgidscardswiththemicrosoftgenericprofilespanelectrical-profile-for-gids-cards-with-the-microsoft-generic-profile"></a><span id="Electrical_Profile_for_GIDS_cards_with_the_Microsoft_Generic_Profile"></span><span id="electrical_profile_for_gids_cards_with_the_microsoft_generic_profile"></span><span id="ELECTRICAL_PROFILE_FOR_GIDS_CARDS_WITH_THE_MICROSOFT_GENERIC_PROFILE"></span>Microsoft の汎用プロファイルで GID のカードの電気のプロファイル


スマート カード、GID の実装のエッジをカードで、受信トレイのクラス ミニドライバーでプロビジョニングできるようにする電気のプロファイルで事前にプロビジョニングする必要があります。 このセクションの情報には、Apdu、データ モデルと GID の仕様で指定されているカードの端の深い理解が必要です。

サブセクションでは、ここでは、パーソナル化のカードを使用する順序で後にする必要があります。 このセクションで参照されている Apdu の詳細については、GID 仕様のセクション 11 を参照してください。

### <a name="span-idgidsapplicationmetadataspanspan-idgidsapplicationmetadataspanspan-idgidsapplicationmetadataspangids-application-metadata"></a><span id="GIDS_Application_Metadata"></span><span id="gids_application_metadata"></span><span id="GIDS_APPLICATION_METADATA"></span>GID アプリケーション メタデータ

このセクションで説明されている、DOs は GID によって管理され、SELECT コマンドの応答のデータ フィールドでのみ取得できます。 このメタデータは、アプリケーションが「作成」状態のときにのみ作成できます。 GID のライフ サイクル管理の詳細については、GID 仕様のセクション 6 を参照してください。

メタデータを以下に注意してくださいには、(ない場合に限る) の説明どおりに存在するに必要なもののみが含まれます。 を省略することも、カード アプリケーションの製造元によってカスタマイズ可能なその他のフィールドがあります。

### <a name="span-idfilecontrolinformationdffcispanspan-idfilecontrolinformationdffcispanspan-idfilecontrolinformationdffcispan-file-control-information-df-fci"></a><span id="_File_Control_Information__DF_FCI_"></span><span id="_file_control_information__df_fci_"></span><span id="_FILE_CONTROL_INFORMATION__DF_FCI_"></span> ファイル制御情報 (DF FCI)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tag</th>
<th align="left">Len</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">64</td>
<td align="left">Var 関数</td>
<td align="left"><p>アプリケーション テンプレートのデータ オブジェクト</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>タグ</dt>
<dd><p>4F</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>Var 関数</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>値</dt>
<dd><p>アプリケーションの補助 =</p>
<p>A0 00 00 03 97 42 54 46 59 xx yy</p>
<ul>
<li><strong>XX</strong> GID 仕様のリビジョン番号が 01 か 02 を = です。</li>
<li><strong>YY</strong> = カード アプリケーション用に予約されています。</li>
</ul>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfilemanagementdatadffmdspanspan-idfilemanagementdatadffmdspanspan-idfilemanagementdatadffmdspan-file-management-data-df-fmd"></a><span id="_File_Management_Data__DF_FMD_"></span><span id="_file_management_data__df_fmd_"></span><span id="_FILE_MANAGEMENT_DATA__DF_FMD_"></span> ファイル管理データ (DF FMD)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tag</th>
<th align="left">Len</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">64</td>
<td align="left">Var 関数</td>
<td align="left"><p>FMD テンプレート</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>タグ</dt>
<dd><p>5F2F</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>Var 関数</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>値</dt>
<dd><p>PIN の使用率ポリシー = (「PIN の使用率ポリシー」を参照してください)</p>
<p>40 または 60 のいずれか</p>
<ul>
<li><strong>40</strong> – アプリケーションの暗証番号 (pin) が存在し、CHV を満たすために使用することがあります。</li>
<li><strong>60</strong> – アプリケーションおよびグローバル ピンは、どちらも存在して、CHV を満たすために使用することがあります。</li>
</ul>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfilecontrolparametersdffcpspanspan-idfilecontrolparametersdffcpspanspan-idfilecontrolparametersdffcpspanfile-control-parameters-df-fcp"></a><span id="File_Control_Parameters__DF_FCP_"></span><span id="file_control_parameters__df_fcp_"></span><span id="FILE_CONTROL_PARAMETERS__DF_FCP_"></span>ファイルの制御パラメーター (DF FCP)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Tag</th>
<th align="left">Len</th>
<th align="left">[値]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">62</td>
<td align="left">Var 関数</td>
<td align="left"><p>FCP テンプレート</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>タグ</dt>
<dd><p>82</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>01</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>値</dt>
<dd><p>ファイル記述子のバイト。38 ("ない共有可能-DF")</p>
</dd>
</dl>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>タグ</dt>
<dd><p>8C</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>03</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>値</dt>
<dd><p>コンパクトな形式でセキュリティ属性 =</p>
<p>03 30 30</p>
<ul>
<li><strong>40</strong>次 – バイトの要件を指定ファイルの作成の EFs とファイルの削除を EFs 用 (とその順序で)。</li>
<li><strong>60</strong> – ユーザー認証、または外部認証は、EFs を作成する要件を満たしています。</li>
<li><strong>60</strong> – ユーザー認証、または外部認証 EFs を削除するための要件を満たすため。</li>
</ul>
<div class="alert">
<strong>注</strong>  セキュリティ属性は、これと完全に一致する必要はありませんが、ユーザー認証、または外部認証を作成および削除の EFs の許可が必要です。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

DF FCP が作成されたら、カードは、以下のセクションで表示するオブジェクトを作成するために必要な状態である「初期化」状態に移行ものとします。

### <a name="span-idpincreationspanspan-idpincreationspanspan-idpincreationspan-pin-creation"></a><span id="_PIN_Creation"></span><span id="_pin_creation"></span><span id="_PIN_CREATION"></span> PIN の作成

PIN を作成するには、アプリケーションのパスワードの変更の参照データ APDU はカードに送信する必要があります。

|            |                              |
|------------|------------------------------|
| CLA        | 00                           |
| アドイン        | 24                           |
| P1         | 01                           |
| P2         | 80                           |
| Lc         | コマンドのデータ フィールドの長さ |
| データ フィールド | &lt;password&gt;             |
| le         | 存在しない場合                       |

 

たとえば、12345678 に PIN を設定するには、次の APDU をカードに送信する必要があります。

``` syntax
00 24 01 80 08 31 32 33 34 35 36 37 38
```

### <a name="span-idpinunblockkeypukcreationspanspan-idpinunblockkeypukcreationspanspan-idpinunblockkeypukcreationspan-pin-unblock-key-puk-creation"></a><span id="_Pin_Unblock_Key__PUK__Creation"></span><span id="_pin_unblock_key__puk__creation"></span><span id="_PIN_UNBLOCK_KEY__PUK__CREATION"></span> Pin のブロックを解除 (PUK) キーの作成

PUK は、ブロック解除や、カードがブロックされたや PIN を忘れた場合は、PIN のリセットに使用されます。 管理者キーのチャレンジ/レスポンスを代わりに使用する場合は、PUK は作成しないでください。

PUK を作成するには、アプリケーション リセット パスワードの変更の参照データ APDU はカードに送信する必要があります。

|            |                              |
|------------|------------------------------|
| CLA        | 00                           |
| アドイン        | 24                           |
| P1         | 01                           |
| P2         | 81                           |
| Lc         | コマンドのデータ フィールドの長さ |
| データ フィールド | &lt;password&gt;             |
| le         | 存在しない場合                       |

 

たとえば、12345678、PUK を設定するには、次の [apdu] をカードに送信する必要があります。

``` syntax
00 24 01 81 08 31 32 33 34 35 36 37 38
```

### <a name="span-idaclcreationspanspan-idaclcreationspanspan-idaclcreationspan-acl-creation"></a><span id="_ACL_Creation"></span><span id="_acl_creation"></span><span id="_ACL_CREATION"></span> ACL の作成

Acl は、作成するファイル [apdu] を使用して作成する必要があります。

|            |                      |
|------------|----------------------|
| CLA        | 00                   |
| アドイン        | E0                   |
| P1、P2      | 00 00                |
| Lc         | データ フィールドの長さ |
| データ フィールド | EF の FCP テンプレート  |
| le         | 存在しない場合               |

 

次の表で説明されている Acl を作成する必要があります。 各 ACL の作成 [apdu] は、ActivateFile APDU (00 44 00 00 00) の後になければなりません

| ACL                      | [APDU]                                                     |
|--------------------------|----------------------------------------------------------|
| UserCreateDeleteDirAc    | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 00 8C 03 03 30 00 |
| EveryoneReadUserWriteAc  | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 10 8C 03 03 30 00 |
| UserWriteExecuteAc       | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 11 8C 03 03 30 FF |
| EveryoneReadAdminWriteAc | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 12 8C 03 03 20 00 |
| UserReadWriteAc          | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 13 8C 03 03 30 30 |
| AdminReadWriteAc         | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 14 8C 03 03 20 20 |

 

### <a name="span-idcreateefforadminkeyspanspan-idcreateefforadminkeyspanspan-idcreateefforadminkeyspan-create-ef-for-admin-key"></a><span id="_Create_EF_for_Admin_Key"></span><span id="_create_ef_for_admin_key"></span><span id="_CREATE_EF_FOR_ADMIN_KEY"></span> EF の管理者キーを作成します。

管理者キーの EF は、作成するファイル [apdu] を使用して作成する必要があります。

|            |                                                |
|------------|------------------------------------------------|
| CLA        | 00                                             |
| アドイン        | E0                                             |
| P1、P2      | 00 00                                          |
| Lc         | データ フィールドの長さ                           |
| データ フィールド | EF の FCP テンプレート (EFID B080 および KeyID の = = 80) |
| le         | 存在しない場合                                         |

 

次の [apdu] は、Triple DES の 3 つのキー管理キーを EF を作成するカードに送信する必要があります。

``` syntax
00 E0 00 00 1C 62 1A 82 01 18 83 02 B0 80 8C 04 87 00 20 FF A5 0B A4 09 80 01 02 83 01 80 95 01 C0
```

上記で説明したコマンドは、ActivateFile APDU 続く必要があります。

``` syntax
00 44 00 00 00
```

### <a name="span-idinjectadminkeyspanspan-idinjectadminkeyspanspan-idinjectadminkeyspan-inject-admin-key"></a><span id="_Inject_Admin_Key"></span><span id="_inject_admin_key"></span><span id="_INJECT_ADMIN_KEY"></span> 管理者キーを挿入します。

管理者キーは、配置キー [apdu] を使用して、カード上に挿入する必要があります。

|            |                      |
|------------|----------------------|
| CLA        | 00                   |
| アドイン        | DB (DB)                   |
| P1、P2      | 3 F FF                |
| Lc         | データ フィールドの長さ |
| データ フィールド | キー使用法のテンプレート   |
| le         | 存在しない場合               |

 

次の [apdu] は、KeyID 80 に、管理者キーを挿入するカードに送信する必要があります。

``` syntax
00 DB 3F FF 26 70 24 84 01 80 A5 1F 87 18 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02
03 04 05 06 07 08 88 03 B0 73 DC
```

上記で説明した例では、次の値を持つ管理者キーを挿入します。

``` syntax
01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08
```

### <a name="span-idsetoperationalstatespanspan-idsetoperationalstatespanspan-idsetoperationalstatespan-set-operational-state"></a><span id="__Set_Operational_State"></span><span id="__set_operational_state"></span><span id="__SET_OPERATIONAL_STATE"></span> 動作状態を設定します。

「運用」の状態の後に EFID と選択の DF「の初期化」状態からカードに移行するには、ファイル アクティブ化コマンドのカードに送信する必要があります。

最初に、DF の選択の APDU を送信します。

|            |        |
|------------|--------|
| CLA        | 00     |
| アドイン        | A4     |
| P1、P2      | 00 0 C  |
| Lc         | 02     |
| データ フィールド | 3 F FF  |
| le         | 存在しない場合 |

 

次に、アクティブ化ファイル [apdu] を使用して、DF の状態を「運用」に変更します。

|            |        |
|------------|--------|
| CLA        | 00     |
| アドイン        | 44     |
| P1、P2      | 00 00  |
| Lc         | 00     |
| データ フィールド | 存在しない場合 |
| le         | 存在しない場合 |

 

次の [apdu] は、運用状態にするカードに送信する必要があります。

``` syntax
00 A4 00 0C 02 3F FF
00 44 00 00 00
```

この手順の後、カードはファイル システムの仕様のセクションで説明したように、ファイル システムを配置するための準備ができてし、「空白カード」と見なされます。 カード「作成」カードのミニドライバー API を使用して、ファイル システムを配置するための手順に従います。 または、Apdu を使用して、カード上のファイル システムを配置するには、次のセクションの手順に従ってください。

### <a name="span-iddataobjectsonagidscardafterthefilesystemiscreatedspanspan-iddataobjectsonagidscardafterthefilesystemiscreatedspanspan-iddataobjectsonagidscardafterthefilesystemiscreatedspan-data-objects-on-a-gids-card-after-the-filesystem-is-created"></a><span id="_Data_objects_on_a_GIDS_card_after_the_filesystem_is_created"></span><span id="_data_objects_on_a_gids_card_after_the_filesystem_is_created"></span><span id="_DATA_OBJECTS_ON_A_GIDS_CARD_AFTER_THE_FILESYSTEM_IS_CREATED"></span> ファイル システムを作成した後は、GID カード上のデータ オブジェクト

カードが Microsoft の一般的なプロファイルと GID の仕様に準拠した、次の表データ オブジェクトとその対応する EFIDs カード「作成」のセクションに従って必須のオブジェクトが作成された後です。 各カードのミニドライバー API が、ファイル システムを作成するために使用されていない場合は、GID 仕様で指定されている配置データ [apdu] を使用するのには、次の表からデータ オブジェクトを配置します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">EFID</th>
<th align="left">タグの操作を行います</th>
<th align="left">目次</th>
<th align="left">フレンドリ名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">A000</td>
<td align="left">DF1F</td>
<td align="left"><pre class="syntax" space="preserve"><code>01 6d 73 63 70 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 a0 00 00 00 00 00
00 00 00 00 00 00 63 61 72 64 69 64 00 00 00 00
00 20 df 00 00 12 a0 00 00 00 00 00 00 00 00 00
00 00 63 61 72 64 61 70 70 73 00 00 00 21 df 00
00 10 a0 00 00 00 00 00 00 00 00 00 00 00 63 61
72 64 63 66 00 00 00 00 00 22 df 00 00 10 a0 00
00 6d 73 63 70 00 00 00 00 00 63 6d 61 70 66 69
6c 65 00 00 00 23 df 00 00 10 a0 00 00</code></pre></td>
<td align="left">マスター ファイル システム テーブル</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF21</td>
<td align="left"><pre class="syntax" space="preserve"><code>6d 73 63 70 00 00 00 00</code></pre></td>
<td align="left">\cardapps</td>
</tr>
<tr class="odd">
<td align="left">A010</td>
<td align="left">DF22</td>
<td align="left"><pre class="syntax" space="preserve"><code>00 00 00 00 00 00</code></pre></td>
<td align="left">\cardcf</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF23</td>
<td align="left"><pre class="syntax" space="preserve"><code>&lt;empty 0-byte data object&gt;</code></pre></td>
<td align="left">mscp\cmapfile</td>
</tr>
<tr class="odd">
<td align="left">A012</td>
<td align="left">DF20</td>
<td align="left"><pre class="syntax" space="preserve"><code>&lt;random 16-byte value&gt;</code></pre></td>
<td align="left">\cardid</td>
</tr>
</tbody>
</table>

 

## <a name="span-idinfsampletore-brandinboxclassminidriverspanspan-idinfsampletore-brandinboxclassminidriverspanspan-idinfsampletore-brandinboxclassminidriverspaninf-sample-to-re-brand-inbox-class-minidriver"></a><span id="INF_Sample_to_re-brand_inbox_class_minidriver"></span><span id="inf_sample_to_re-brand_inbox_class_minidriver"></span><span id="INF_SAMPLE_TO_RE-BRAND_INBOX_CLASS_MINIDRIVER"></span>受信トレイ クラス ミニドライバーの再ブランド化する INF サンプル


スマート カード ベンダーは、ドライバー パッケージを配布するのにことがなく、受信トレイ ミニドライバーを使用できます。 このようなカードのプラグ アンド プレイ エクスペリエンスには、ブランド情報を追加するには、ベンダーがブランド化の情報を提供するさまざまな文字列をオーバーライドする INF ファイルを提供できます。 これらの文字列を以下に示します。

-   ProviderName
-   CardDeviceName
-   SmartCardName

次に受信トレイ ミニドライバーで使用できるサンプル INF ファイルを示します。 この INF ファイルは、x86 と amd64 の CPU プラットフォームでのインストールに修飾されます。

``` syntax
;
;FabrikamVendor Smartcard Minidriver for an x86 and x64 based package.
;

[Version]
Signature="$Windows NT$"
Class=SmartCard
ClassGuid={990A2BD7-E738-46c7-B26F-1CF8FB9F1391}
Provider=%ProviderName%
CatalogFile=delta.cat
DriverVer=10/03/2009,10.0.0.1

[Manufacturer]
%ProviderName%=Minidriver,NTamd64,NTamd64.6.1,NTx86,NTx86.6.1

[Minidriver.NTamd64]
%CardDeviceName%=Minidriver64_Install,SCFILTER\CID_51FF0800

[Minidriver.NTx86]
%CardDeviceName%=Minidriver32_Install,SCFILTER\CID_51FF0800

[Minidriver.NTamd64.6.1]
%CardDeviceName%=Minidriver64_61_Install,SCFILTER\CID_51FF0800

[Minidriver.NTx86.6.1]
%CardDeviceName%=Minidriver32_61_Install,SCFILTER\CID_51FF0800

[DefaultInstall]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64.6.1]
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86.6.1]
AddReg=AddRegDefault

[SourceDisksFiles]
msclmd64.dll=1
msclmd.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[Minidriver64_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[Minidriver64_61_Install.NT]
AddReg=AddRegWOW64
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[Minidriver32_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[Minidriver32_61_Install.NT]
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[Minidriver64_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services

[Minidriver32_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services


[Minidriver64_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[Minidriver64_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[Minidriver64_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[Minidriver32_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[Minidriver32_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[Minidriver32_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[amd64_CopyFiles]
msclmd.dll,msclmd64.dll

[x86_CopyFiles]
msclmd.dll

[wow64_CopyFiles]
msclmd.dll

[AddRegWOW64]
HKLM, %SmartCardNameWOW64%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardNameWOW64%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardNameWOW64%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardNameWOW64%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardNameWOW64%,"80000001",0x00000000,%SmartCardCardModule%

[AddRegDefault]
HKLM, %SmartCardName%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardName%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardName%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardName%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardName%,"80000001",0x00000000,%SmartCardCardModule%

[DestinationDirs]
amd64_CopyFiles=10,system32
x86_CopyFiles=10,system32
wow64_CopyFiles=10,syswow64


; =================== Generic ==================================

[Strings]
ProviderName ="FabrikamVendor"
MediaDescription="FabrikamVendor Smart Card Minidriver Installation Disk"
CardDeviceName="FabrikamVendor Minidriver for Smart Card"
SmartCardName="SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardNameWOW64="SOFTWARE\Wow6432Node\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardCardModule="msclmd.dll"
```

次に、この種類の INF ファイルに必要です。

-   デバイスの ATR 履歴バイトまたはデバイスのスマート カード フレームワークの識別子のデコードされた値にする必要があります %fabrikamcarddevicename% 文字列によって指定されているハードウェア ID。 この識別子の詳細については、「Windows スマート カード フレームワーク カード識別子」のセクションを参照してください。[検出プロセス](discovery-process.md)します。
-   **DefaultInstall**スマート カード ミニドライバーのパッケージは、INF ファイルのセクションは必須です。
-   **DriverVer** INF ファイルのディレクティブは、受信トレイのドライバーの INF ファイルのバージョンとタイムスタンプの値より大きい値をいる必要があります。 それ以外の場合、システムは、ベンダーの INF ファイルを使用して、デバイスをインストールされません。

    **DriverVer**ディレクティブは、次の構文。

    ``` syntax
    DriverVer=mm/dd/yyyy[,w.x.y.z]
    ```

    値を設定するときに、これらのガイドラインに従うことをお勧め、 **DriverVer**ディレクティブ。

    -   Windows サービス パックの更新プログラムとの競合を防ぐために将来に十分である日付の値を指定します。
    -   4 桁のバージョン番号は省略可能ですが、受信トレイのドライバーの INF ファイルで指定されている現在のバージョンよりも大幅に高くなっているバージョンを指定する必要があります。

INF ファイルと構文の詳細については、次を参照してください。[デバイスとドライバーのインストールの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)します。

 

 





