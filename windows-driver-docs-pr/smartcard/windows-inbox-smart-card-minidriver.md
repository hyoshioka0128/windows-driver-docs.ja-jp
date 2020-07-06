---
title: Windows Inbox スマート カード ミニドライバー
description: Windows Inbox スマート カード ミニドライバー
ms.assetid: 4B61607E-090A-4935-B944-110ACE9A4D83
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 266be9f0091b0f41e622c7384fd1daf94535b368
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968501"
---
# <a name="windows-inbox-smart-card-minidriver"></a>Windows Inbox スマート カード ミニドライバー


Windows 7 Service Pack 1 (SP1) 以降では、PIV 準拠のスマートカードと、GID カードのエッジを実装するカードをサポートする受信トレイの汎用クラスミニドライバーが提供されています。

PIV 準拠のスマートカードと、GID カードのエッジを実装するカード。 PIV の詳細については、[連邦社員および請負業者の個人 id の確認 (PIV) に関する](http://csrc.nist.gov/groups/SNS/piv/index.mdl)web ページを参照してください。

GID の詳細については、「[汎用 Id デバイス仕様](https://msdn.microsoft.com/windows/hardware/gg487496)」 web ページを参照してください。

スマートカードがリーダーに挿入され、Base CSP/KSP が[**CardAcquireContext**](https://docs.microsoft.com/previous-versions/dn468701(v=vs.85))を呼び出すと、ミニドライバークラスは次の検出プロセスを実行して、関連付けられているカードを PIV または gid 準拠としてマークします。

1.  SELECT コマンドは、PIV エイドを見つけるために発行されます。 コマンドが成功した場合、Windows はカードを PIV デバイスと見なし、検出プロセスを停止します。
2.  コマンドが失敗した場合は、SELECT コマンドを実行して、GID 支援を見つけます。 コマンドが成功した場合、Windows はカードが GID デバイスであると見なされ、検出プロセスは停止します。
3.  スマートカード上に補助がないことを示すステータスコードでコマンドが失敗した場合、Windows は、カードが GID デバイスであるかのように処理を続行します。 他のエラーが発生してコマンドが失敗した場合、Windows はカードを不明なデバイスと見なします。

## <a name="span-idelectrical_profile_for_gids_cards_with_the_microsoft_generic_profilespanspan-idelectrical_profile_for_gids_cards_with_the_microsoft_generic_profilespanspan-idelectrical_profile_for_gids_cards_with_the_microsoft_generic_profilespanelectrical-profile-for-gids-cards-with-the-microsoft-generic-profile"></a><span id="Electrical_Profile_for_GIDS_cards_with_the_Microsoft_Generic_Profile"></span><span id="electrical_profile_for_gids_cards_with_the_microsoft_generic_profile"></span><span id="ELECTRICAL_PROFILE_FOR_GIDS_CARDS_WITH_THE_MICROSOFT_GENERIC_PROFILE"></span>Microsoft 汎用プロファイルを使用した、GID カードの電気プロファイル


GID カードエッジを実装するスマートカードの場合は、受信トレイクラスミニドライバーを使用してプロビジョニングできるようにするための電気プロファイルを事前にプロビジョニングする必要があります。 このセクションの情報を参照するには、GID 仕様で指定されている APDUs、データモデル、およびカードエッジを深く理解しておく必要があります。

ここで指定するサブセクションは、個人用設定にカードを使用する前に記載されている順序に従う必要があります。 このセクションで参照されている APDUs の詳細については、「GID 仕様」のセクション11を参照してください。

### <a name="span-idgids_application_metadataspanspan-idgids_application_metadataspanspan-idgids_application_metadataspangids-application-metadata"></a><span id="GIDS_Application_Metadata"></span><span id="gids_application_metadata"></span><span id="GIDS_APPLICATION_METADATA"></span>GID アプリケーションメタデータ

このセクションで説明する DOs は、GID によって管理されており、SELECT コマンドの response data フィールドでのみ取得できます。 このメタデータは、アプリケーションが "作成" 状態のときにのみ作成できます。 GID ライフサイクル管理の詳細については、GID 仕様のセクション6を参照してください。

以下のメタデータには、説明どおりに正確に提示する必要があるもののみが含まれていることに注意してください (特に明記されていない場合)。 その他のフィールドは省略可能であり、カードアプリケーションベンダーがカスタマイズできます。

### <a name="span-id_file_control_information__df_fci_spanspan-id_file_control_information__df_fci_spanspan-id_file_control_information__df_fci_span-file-control-information-df-fci"></a><span id="_File_Control_Information__DF_FCI_"></span><span id="_file_control_information__df_fci_"></span><span id="_FILE_CONTROL_INFORMATION__DF_FCI_"></span>ファイル制御情報 (DF FCI)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">タグ</th>
<th align="left">Len</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">64</td>
<td align="left">Var.</td>
<td align="left"><p>アプリケーションテンプレートデータオブジェクト</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>番号</dt>
<dd><p>4F</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>Var.</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>数値</dt>
<dd><p>アプリケーション補助 =</p>
<p>A0 00 00 03 97 42 54 46 59 xx yy</p>
<ul>
<li><strong>XX</strong> = gid 指定のリビジョン番号 (01 または 02)。</li>
<li><strong>YY</strong> = カードアプリケーション用に予約されています。</li>
</ul>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

### <a name="span-id_file_management_data__df_fmd_spanspan-id_file_management_data__df_fmd_spanspan-id_file_management_data__df_fmd_span-file-management-data-df-fmd"></a><span id="_File_Management_Data__DF_FMD_"></span><span id="_file_management_data__df_fmd_"></span><span id="_FILE_MANAGEMENT_DATA__DF_FMD_"></span>ファイル管理データ (DF FMD)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">タグ</th>
<th align="left">Len</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">64</td>
<td align="left">Var.</td>
<td align="left"><p>FMD テンプレート</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>番号</dt>
<dd><p>5F2F</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>Var.</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>数値</dt>
<dd><p>PIN 使用ポリシー (「PIN Usage Policy」を参照してください) =</p>
<p>40または60</p>
<ul>
<li><strong>40</strong> –アプリケーション PIN は存在し、chv を満たすために使用できます。</li>
<li><strong>60</strong> –アプリケーションとグローバルの pin は両方とも存在し、chv を満たすために使用できます。</li>
</ul>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfile_control_parameters__df_fcp_spanspan-idfile_control_parameters__df_fcp_spanspan-idfile_control_parameters__df_fcp_spanfile-control-parameters-df-fcp"></a><span id="File_Control_Parameters__DF_FCP_"></span><span id="file_control_parameters__df_fcp_"></span><span id="FILE_CONTROL_PARAMETERS__DF_FCP_"></span>ファイル制御パラメーター (DF FCP)

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">タグ</th>
<th align="left">Len</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">62</td>
<td align="left">Var.</td>
<td align="left"><p>FCP テンプレート</p>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>番号</dt>
<dd><p>82</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>01</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>数値</dt>
<dd><p>ファイル記述子のバイト:38 ("共有不可能-DF")</p>
</dd>
</dl>
<p></p>
<dl>
<dt><span id="Tag"></span><span id="tag"></span><span id="TAG"></span>番号</dt>
<dd><p>8C</p>
</dd>
<dt><span id="Len"></span><span id="len"></span><span id="LEN"></span>Len</dt>
<dd><p>03</p>
</dd>
<dt><span id="Value"></span><span id="value"></span><span id="VALUE"></span>数値</dt>
<dd><p>Compact 形式のセキュリティ属性 =</p>
<p>03 30 30</p>
<ul>
<li><strong>40</strong> –次のバイトは、EFS の作成ファイルと EFS の削除ファイル (およびその順序) の要件を指定します。</li>
<li><strong>60</strong> –ユーザー認証または外部認証は、EFs を作成するための要件を満たしています。</li>
<li><strong>60</strong> –ユーザー認証または外部認証は、EFs を削除するための要件を満たしています。</li>
</ul>
<div class="alert">
<strong>メモ</strong>   Security 属性はこの値と正確に一致する必要はありませんが、EFs の作成と削除の両方に対するユーザー認証または外部認証が許可されている必要があります。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
</tbody>
</table>

 

DF FCP が作成されると、カードは "初期化" 状態に移行します。これは、次のセクションに示すオブジェクトの作成に必要な状態です。

### <a name="span-id_pin_creationspanspan-id_pin_creationspanspan-id_pin_creationspan-pin-creation"></a><span id="_PIN_Creation"></span><span id="_pin_creation"></span><span id="_PIN_CREATION"></span>PIN の作成

PIN を作成するには、アプリケーションパスワードの変更参照データをカードに送信する必要があります。

**Cla**:00

**INS**:24

**P1**:01

**P2**:80

**Lc**: コマンドデータフィールドの長さ

**データフィールド**: &lt; パスワード&gt;

**Le**: 存在しない


 

たとえば、PIN を12345678に設定するには、次の APDU をカードに送信する必要があります。

``` syntax
00 24 01 80 08 31 32 33 34 35 36 37 38
```

### <a name="span-id_pin_unblock_key__puk__creationspanspan-id_pin_unblock_key__puk__creationspanspan-id_pin_unblock_key__puk__creationspan-pin-unblock-key-puk-creation"></a><span id="_Pin_Unblock_Key__PUK__Creation"></span><span id="_pin_unblock_key__puk__creation"></span><span id="_PIN_UNBLOCK_KEY__PUK__CREATION"></span>Pin のブロック解除キー (PUK) の作成

PUK は、カードがブロックされるか、PIN が忘れられた場合に、PIN のブロック解除とリセットに使用されます。 代わりに管理者キーチャレンジ/応答を使用する場合は、PUK を作成しないでください。

PUK を作成するには、パスワードをリセットするための変更参照データ APDU をカードに送信する必要があります。

**Cla**:00

**INS**:24

**P1**:01

**P2**:81

**Lc**: コマンドデータフィールドの長さ

**データフィールド**: &lt; パスワード&gt;

**Le**: 存在しない


 

たとえば、PUK を12345678に設定するには、次の APDU をカードに送信する必要があります。

``` syntax
00 24 01 81 08 31 32 33 34 35 36 37 38
```

### <a name="span-id_acl_creationspanspan-id_acl_creationspanspan-id_acl_creationspan-acl-creation"></a><span id="_ACL_Creation"></span><span id="_acl_creation"></span><span id="_ACL_CREATION"></span>ACL の作成

Acl は、CREATE FILE APDU を使用して作成する必要があります。

**Cla**:00

**INS**: E0

**P1-P2**:00 00

**Lc**: データフィールドの長さ

**データフィールド**: EF の FCP テンプレート

**Le**: 存在しない


 

次の表に示されている Acl を作成する必要があります。 各 ACL 作成 APDU の後に、アクティブファイル APDU (00 44 00 00 00) を指定する必要があります。

| .ACL                      | APDU                                                     |
|--------------------------|----------------------------------------------------------|
| UserCreateDeleteDirAc    | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 00 8C 03 03 30 00 |
| すべてのユーザーの Onereaduserwriteac  | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 10 8C 03 03 30 00 |
| UserWriteExecuteAc       | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 11 8C 03 03 30 FF |
| すべての Onereadadminwriteac | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 12 8C 03 03 20 00 |
| UserReadWriteAc          | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 13 8C 03 03 30 30 |
| AdminReadWriteAc         | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 14 8C 03 03 20 20 |

 

### <a name="span-id_create_ef_for_admin_keyspanspan-id_create_ef_for_admin_keyspanspan-id_create_ef_for_admin_keyspan-create-ef-for-admin-key"></a><span id="_Create_EF_for_Admin_Key"></span><span id="_create_ef_for_admin_key"></span><span id="_CREATE_EF_FOR_ADMIN_KEY"></span>管理者キーの EF を作成する

Admin キーの EF は、CREATE FILE APDU を使用して作成する必要があります。

**Cla**:00

**INS**: E0

**P1-P2**:00 00

**Lc**: データフィールドの長さ

**データフィールド**: EF の FCP テンプレート (Efid = B080 およびキー id = 80)

**Le**: 存在しない


 

Triple DES 3 キー管理キーの EF を作成するには、次の APDU をカードに送信する必要があります。

``` syntax
00 E0 00 00 1C 62 1A 82 01 18 83 02 B0 80 8C 04 87 00 20 FF A5 0B A4 09 80 01 02 83 01 80 95 01 C0
```

上記のコマンドの後に、次のようなファイルの APDU を指定する必要があります。

``` syntax
00 44 00 00 00
```

### <a name="span-id_inject_admin_keyspanspan-id_inject_admin_keyspanspan-id_inject_admin_keyspan-inject-admin-key"></a><span id="_Inject_Admin_Key"></span><span id="_inject_admin_key"></span><span id="_INJECT_ADMIN_KEY"></span>管理者キーの挿入

PUT KEY APDU を使用して、管理者キーをカードに挿入する必要があります。

**Cla**:00

**INS**: DB

**P1-P2**: 3f FF

**Lc**: データフィールドの長さ

**データフィールド**: キー使用法テンプレート

**Le**: 存在しない


 

次の APDU をカードに送信して、管理者キーをキー Id 80 に挿入する必要があります。

``` syntax
00 DB 3F FF 26 70 24 84 01 80 A5 1F 87 18 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02
03 04 05 06 07 08 88 03 B0 73 DC
```

前述の例では、管理者キーが次の値で挿入されます。

``` syntax
01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08
```

### <a name="span-id__set_operational_statespanspan-id__set_operational_statespanspan-id__set_operational_statespan-set-operational-state"></a><span id="__Set_Operational_State"></span><span id="__set_operational_state"></span><span id="__SET_OPERATIONAL_STATE"></span>動作状態の設定

カードを "初期化" 状態から "操作中" 状態に遷移させるには、SELECT DF with EFID の後に ACTIVATE FILE コマンドを実行する必要があります。

まず、DF の SELECT APDU を送信します。

**Cla**:00

**INS**: A4

**P1-P2**:00 0c

**Lc**:02

**データフィールド**: 3f FF

**Le**: 存在しない


 

次に、ACTIVATE FILE APDU を使用して、DF の状態を "operational" に変更します。

**Cla**:00

**INS**:44

**P1-P2**:00 00

**Lc**:00

**データフィールド**: 存在しない

**Le**: 存在しない


 

次の APDU をカードに送信して、動作状態にする必要があります。

``` syntax
00 A4 00 0C 02 3F FF
00 44 00 00 00
```

この手順の後、カードは「ファイルシステムの仕様」で説明されているようにファイルシステムを配置する準備ができ、"空のカード" と見なされます。 カードの「作成」の手順に従って、ミニドライバー API を使用してカードにファイルシステムを配置します。 または、次のセクションの手順に従って、APDUs を使用してファイルシステムをカードに配置します。

### <a name="span-id_data_objects_on_a_gids_card_after_the_filesystem_is_createdspanspan-id_data_objects_on_a_gids_card_after_the_filesystem_is_createdspanspan-id_data_objects_on_a_gids_card_after_the_filesystem_is_createdspan-data-objects-on-a-gids-card-after-the-filesystem-is-created"></a><span id="_Data_objects_on_a_GIDS_card_after_the_filesystem_is_created"></span><span id="_data_objects_on_a_gids_card_after_the_filesystem_is_created"></span><span id="_DATA_OBJECTS_ON_A_GIDS_CARD_AFTER_THE_FILESYSTEM_IS_CREATED"></span>ファイルシステムが作成された後の、GID カード上のデータオブジェクト

Microsoft 汎用プロファイルでの GID 仕様に準拠したカードの場合、次の表では、カード "作成" のセクションに従って、必須オブジェクトが作成された後のデータオブジェクトとそれに対応する EFIDs について説明します。 ミニドライバー API がファイルシステムの作成に使用されていない場合は、GID 仕様で指定されている PUT DATA APDU を使用して、以下の表の各データオブジェクトをカードに配置します。

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
<th align="left">DO タグ</th>
<th align="left">内容</th>
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
<td align="left">マスターファイルシステムテーブル</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF21</td>
<td align="left"><pre class="syntax" space="preserve"><code>6d 73 63 70 00 00 00 00</code></pre></td>
<td align="left">\ cardapps</td>
</tr>
<tr class="odd">
<td align="left">A010</td>
<td align="left">DF22</td>
<td align="left"><pre class="syntax" space="preserve"><code>00 00 00 00 00 00</code></pre></td>
<td align="left">\ cardcf</td>
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
<td align="left">\ cardid</td>
</tr>
</tbody>
</table>

 

## <a name="span-idinf_sample_to_re-brand_inbox_class_minidriverspanspan-idinf_sample_to_re-brand_inbox_class_minidriverspanspan-idinf_sample_to_re-brand_inbox_class_minidriverspaninf-sample-to-re-brand-inbox-class-minidriver"></a><span id="INF_Sample_to_re-brand_inbox_class_minidriver"></span><span id="inf_sample_to_re-brand_inbox_class_minidriver"></span><span id="INF_SAMPLE_TO_RE-BRAND_INBOX_CLASS_MINIDRIVER"></span>再ブランド化されるミニドライバークラスの INF サンプル


スマートカードのベンダーは、ドライバーパッケージを出荷しなくても、受信トレイミニドライバーを使用できます。 このようなカードのプラグアンドプレイエクスペリエンスにブランド情報を追加するために、ベンダーは、さまざまな文字列をオーバーライドしてブランド情報を提供する INF ファイルを提供できます。 これらの文字列には次のものが含まれます。

-   ProviderName
-   CardDeviceName
-   SmartCardName

次に示すのは、受信トレイミニドライバーで使用できる INF ファイルのサンプルです。 この INF ファイルは、x86 および amd64 CPU プラットフォームでのインストールのために装飾されています。

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

この種類の INF ファイルには、次のものが必要です。

-   % FabrikamCardDeviceName% 文字列で指定されたハードウェア ID は、デバイスの ATR 履歴バイトまたはデバイスのスマートカードフレームワーク識別子のデコードされた値のいずれかである必要があります。 この識別子の詳細については、「[検出プロセス](discovery-process.md)」の「Windows スマートカードフレームワークカード識別子」セクションを参照してください。
-   **DefaultInstall**セクションは、スマートカードミニドライバーパッケージの INF ファイルでは必須です。
-   INF ファイルの**DriverVer**ディレクティブには、受信トレイドライバーの INF ファイルのバージョンおよびタイムスタンプ値よりも大きい値を指定する必要があります。 それ以外の場合、システムはベンダーの INF ファイルを使用してデバイスをインストールしません。

    **DriverVer**ディレクティブには、次の構文があります。

    ``` syntax
    DriverVer=mm/dd/yyyy[,w.x.y.z]
    ```

    **DriverVer**ディレクティブの値を設定するときは、次のガイドラインに従うことをお勧めします。

    -   Windows Service Pack の更新との競合を避けるために、将来の日付の値を指定してください。
    -   4桁のバージョン番号は省略可能ですが、受信トレイドライバーの INF ファイルで指定されている現在のバージョンよりも大幅に大きいバージョンを指定する必要があります。

INF ファイルと構文の詳細については、「[デバイスとドライバーのインストールの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)」を参照してください。

 

 





