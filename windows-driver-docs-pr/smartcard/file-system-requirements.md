---
title: ファイル システムの要件
description: ファイル システムの要件
ms.assetid: 2C363978-3C98-4838-8C55-F804D2C75BEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 424034f664a66d3e168cc218298e21eee8ca0a9b
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563162"
---
# <a name="file-system-requirements"></a>ファイル システムの要件


"論理" レイアウトは、基本 CSP/KSP に提示されたデータレイアウトです。 このレイアウトでは、人が判読できる名前を使用します。ファイルは、カードが使用する物理的なレイアウト内のファイルと1対1で対応していない可能性があります。

## <a name="span-idfile_naming_requirementsspanspan-idfile_naming_requirementsspanspan-idfile_naming_requirementsspanfile-naming-requirements"></a><span id="File_Naming_Requirements"></span><span id="file_naming_requirements"></span><span id="FILE_NAMING_REQUIREMENTS"></span>ファイルの名前付け要件


ファイル名は、最大8つの ANSI 文字 (8 ビット) で構成され、Windows ファイルとディレクトリの名前付け規則で許可されていない文字は除外されます。 ディレクトリ構造は、ルートディレクトリとアプリケーションが使用するディレクトリの2つのレベルで構成されます。 ディレクトリ名は、最大8つの ANSI 文字で構成されます。 大文字と小文字が区別されないファイル名とディレクトリ名を生成するには、カードミニドライバーの実装で文字列を小文字に変換する必要があります。

## <a name="span-idfile_naming_virtualizationspanspan-idfile_naming_virtualizationspanspan-idfile_naming_virtualizationspanfile-naming-virtualization"></a><span id="File_Naming_Virtualization"></span><span id="file_naming_virtualization"></span><span id="FILE_NAMING_VIRTUALIZATION"></span>ファイルの名前付けの仮想化


カードミニドライバーには、ディレクトリとファイルをカード上の適切な場所にマップする仮想ファイルシステムを実装することができます。 通常の操作 (National ID カードなど) の実行中に書き込み操作が許可されていないカードは、書き込み操作をシミュレートできますが、カードの挿入中に "書き込まれた" ファイルを保持し、読み取り時にこれらのファイルを返すことができるようにする必要があります。

## <a name="span-id_physical_card_data_layoutspanspan-id_physical_card_data_layoutspanspan-id_physical_card_data_layoutspan-physical-card-data-layout"></a><span id="_Physical_Card_Data_Layout"></span><span id="_physical_card_data_layout"></span><span id="_PHYSICAL_CARD_DATA_LAYOUT"></span>物理カードのデータレイアウト


カード上のファイルに関する次の情報は、カードとファイルシステムの使用方法の概要です。 カードミニドライバーは、これらのファイルまたはその内容についての知識を使用して設計する必要があります。 カードミニドライバーは一般化されたインターフェイスレイヤーとして記述する必要があります。

## <a name="span-idlogical_data_layoutspanspan-idlogical_data_layoutspanspan-idlogical_data_layoutspanlogical-data-layout"></a><span id="Logical_Data_Layout"></span><span id="logical_data_layout"></span><span id="LOGICAL_DATA_LAYOUT"></span>論理データレイアウト


### <a name="span-idcard_identifierspanspan-idcard_identifierspanspan-idcard_identifierspancard-identifier"></a><span id="Card_Identifier"></span><span id="card_identifier"></span><span id="CARD_IDENTIFIER"></span>カード識別子

カード識別子は、カードの一意の識別子です。 UI では、何らかの形式でユーザーに表示される場合がありますが、それ以外の場合は、カードの id を確立するための参照値との比較にのみ使用されます。 この値は、カードがユーザーに対して準備されるときに割り当てられます。 バイト配列として構成されています。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>ファイル名  
このファイルの論理名は "CardId" です。 ルートディレクトリにあります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E (R)、U (R)、および A (RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
ファイルは16バイト配列として編成されます。 これは、不透明なバイナリデータとして処理する必要があります。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
この値は、カードに対して一意の値が生成されることを保証するために、Microsoft ソフトウェアによって割り当てられます。 これは、製造時にカードに割り当てられることがない、シリアル番号とは無関係です。

### <a name="span-idapplication_directoryspanspan-idapplication_directoryspanspan-idapplication_directoryspanapplication-directory"></a><span id="Application_Directory"></span><span id="application_directory"></span><span id="APPLICATION_DIRECTORY"></span>アプリケーションディレクトリ

アプリケーションディレクトリファイルは、固定長のアプリケーション名エントリの一覧で構成されます。 アプリケーションディレクトリ名は、アプリケーションのすべてのファイルを含む論理サブディレクトリの名前です。 CAPI2 を使用するアプリケーションの場合、名前は "mscp" で、インデックス値は0です。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>論理名  
このファイルの論理名は "cardapps" です。 ルートディレクトリにあります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E (R)、U (RW)、および A (RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
ファイルは、バイトインデックスの後にゼロで終わるアプリケーション名文字列 (ANSI) を含む一連のレコードとして編成されます。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
アプリケーションの実装では、アプリケーション名がカード上の一意のディレクトリにマップされていることと、カードキャッシュファイル内のアプリケーションデータの一意のインデックスに対応していることが必要です。 カードアプリケーションディレクトリを使用すると、アプリケーションディレクトリで名前を検索し、その位置のインデックスを記録することによって、アプリケーションがキャッシュファイル内のインデックス値を見つけることができます。 このファイルは、アプリケーション名を含む8バイトのレコードで構成され、最後にゼロが入力されます。 アプリケーション名には、8バイトすべてを使用できます。これにより、結果の文字列をゼロで終了する必要がなくなります。 このため、"created" カードのファイルの内容は、次の8バイトになります。

``` syntax
{‘mscp’,0,0,0,0}
```

### <a name="span-idcache_filespanspan-idcache_filespanspan-idcache_filespancache-file"></a><span id="Cache_File"></span><span id="cache_file"></span><span id="CACHE_FILE"></span>キャッシュファイル

パフォーマンスを向上させ、カードとの通信を減らすために、基本 CSP/KSP はさまざまな方法でカードデータをキャッシュできます。 キャッシュファイルは、カード上のデータのバージョン番号を示すことによって、ベース CSP/KSP 内のキャッシュサブシステムの操作を制御するために使用されます。 データが変更されると、この値はインクリメントされます。 キャッシュファイルの内部コピーをカードから読み取られたバージョンと比較すると、基本 CSP/KSP は、キャッシュされたデータを使用できるか更新する必要があるかを判断できます。 この決定は、カードの取り出しや挿入など、さまざまな理由で発生する可能性があります。

カードからカード識別子とキャッシュファイルを読み取るには、ホストで不確定期間にキャッシュされた情報を使用できるようにするだけで十分です。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>論理名  
このファイルの論理名は "CardCF" です。 ルートディレクトリにあります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E (R)、U (RW)、および A (RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
このファイルは、グローバルデータを2バイト値の形式で整理し、アプリケーションが保持および解釈する32ビットのキャッシュ値を連続して構成します。 最初の部分は、基本 CSP/KSP が使用するために予約されています。 その後、各アプリケーションに1つの**DWORD**が割り当てられます。

``` syntax
typedef struct _CARD_CACHE_FILE_FORMAT
{
    BYTE bVersion;          // Cache version
    BYTE bPinsFreshness;        // Card PIN
    WORD wContainersFreshness;
    WORD wFilesFreshness;

} CARD_CACHE_FILE_FORMAT, *PCARD_CACHE_FILE_FORMAT;
```

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
アプリケーション内部キャッシュは、アプリケーションの内部にあるキャッシュデータコピーが、カードから読み取られたファイルよりも関心のあるデータに対して異なるバージョン番号を示す場合に更新されます。 通常、キャッシュはカードを使用した各トランザクションの開始時にチェックされます。

アプリケーションキャッシュデータの Dword の配列 (キャッシュアプリケーションごとに1つ) には、アプリケーションのディレクトリファイルのアプリケーションインデックスによってインデックスが作成されます。 アプリケーションが追加されると、ファイルは4バイト単位で増加します。

### <a name="span-idcontainer_map_filespanspan-idcontainer_map_filespanspan-idcontainer_map_filespancontainer-map-file"></a><span id="Container_Map_File"></span><span id="container_map_file"></span><span id="CONTAINER_MAP_FILE"></span>コンテナーマップファイル

コンテナーマップファイルは、Base CSP/KSP によって所有されており、CONTAINERMAPRECORD 型の複数のレコードで構成されています。 これらのレコードは、コンテナー識別子を関連付けます。通常、この識別子は、CAPI によって割り当てられた GUID であり、そのコンテナーのキーと証明書にアクセスするために使用できるインデックスに関連付けられています。

ファイル内のレコードの位置 (インデックス) は、そのコンテナーに関連付けられている証明書とキー情報のインデックスに対応します。 このため、このようなファイルの2番目のレコードには、0から始まるインデックス1が表示されます。

このコンテナーに関連付けられている証明書と、コンテナーの署名キーまたはキー交換キーによって、このインデックス (UserCerts \\ SignatureCert1、SignatureKey1 など) が共有されます。 レコードには、そのインデックスに関連付けられているキーのコンテナー GUID とサイズ情報が含まれています。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>論理名  
このファイルの論理名は "CMapFile" です。 これは "mscp" ディレクトリにあります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E (R)、U (RW)、および A (RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
このファイルのアクセス条件は、E (R)、U (RW)、および A (RW) です。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
このファイルは、基本 CSP/KSP によって作成され、そのコンテンツが保持されます。 このファイルの内部構造に関する情報は、参照専用として提供されています。 ファイル内のレコードの形式は次のとおりです。

**CONTAINERMAPRECORD**

これらのレコードには、CAPI によって割り当てられたコンテナー GUID と、そのコンテナーに関連付けられている関連キー交換キーまたは署名キーのキーサイズが含まれます。 すべての単語メンバーは、Endean バイト順です。

``` syntax
//
// Type: CONTAINER_MAP_RECORD
//
// This structure describes the format of the Base CSP's 
// container map file, stored on the card. This is well-known 
// logical file wszCONTAINER_MAP_FILE. The file consists of 
// zero or more of these records.
//
#define MAX_CONTAINER_NAME_LEN                  39

// This flag is set in the CONTAINER_MAP_RECORD bFlags 
// member if the corresponding container is valid and currently 
// exists on the card. // If the container is deleted, its 
// bFlags field must be cleared.
#define CONTAINER_MAP_VALID_CONTAINER           1

// This flag is set in the CONTAINER_MAP_RECORD bFlags
// member if the corresponding container is the default
// container on the card.
define CONTAINER_MAP_DEFAULT_CONTAINER         2

typedef struct _CONTAINER_MAP_RECORD
{
    WCHAR wszGuid [MAX_CONTAINER_NAME_LEN + 1];
    BYTE bFlags;
    BYTE bReserved;
    WORD wSigKeySizeBits;
    WORD wKeyExchangeKeySizeBits;
} CONTAINER_MAP_RECORD, *PCONTAINER_MAP_RECORD;
```

**WszGuid**メンバーは、CAPI によってコンテナーに割り当てられた識別子の UNICODE 文字列形式で構成されます。 これは通常、GUID 文字列ではありませんが、常にであるとは限りません。 識別子名に特殊文字 "" を含めることはできません \\ 。 読み取り専用カードをプロビジョニングする場合、プロビジョニングプロセスは識別子名と同じガイドラインに従う必要があります。

コンテナー名は null で終わる必要があり、null \_ \_ \_ 終端文字を含む長さ (コンテナー名の LEN + 1) 文字以下でなければなりません。

レコードをこのテーブルから削除する必要がある場合、レコードにゼロを書き込むことによってエントリが無効になります。 このようなレコードは、後で新しいデータによって上書きされる可能性があります。 非アクティブなエントリを削除するために、テーブルが "パック" されていません。

次のビットは、フラグバイトに対して有効です。

-   ビット0は、コンテナーレコードが有効な場合に設定されます。
-   ビット1は、コンテナーが既定値の場合に設定されます。 このビットは、コンテナーマップ内の1つのレコードに対していつでも設定できます。 このビットは、ビット0も設定されている場合にのみ設定できます。 つまり、既定のコンテナーを無効にすることはできません。 その他のすべてのビットは、現在、カードミニドライバーの将来のリビジョン用に予約されています。
-   既定のコンテナーの場合、これはバイト0x03 に変換されます。 既定値ではない有効なコンテナーの場合、この値は0x01 になります。
-   Bits 2-7 は将来使用するために予約されています。

## <a name="span-iddata_layout_summaryspanspan-iddata_layout_summaryspanspan-iddata_layout_summaryspandata-layout-summary"></a><span id="Data_Layout_Summary"></span><span id="data_layout_summary"></span><span id="DATA_LAYOUT_SUMMARY"></span>データレイアウトの概要


次の表は、一般的な実装のためのカードミニドライバーと基本 CSP/KSP との間のインターフェイスにおけるデータの編成をまとめたものです。 "論理名" は、基本 CSP/KSP がカードミニドライバーとの通信に使用する文字列です。カード上の対応する要素に直接マップする場合もあれば、そうでない場合もあります。

証明書とキーは、基本 CSP/KSP によって、実際のファイル名のインデックスのみを使用して、目的に応じてサブディレクトリに論理的にグループ化されていることに注意してください。 カードに追加された証明書またはキーには、ディレクトリ内のインデックス番号に基づいて名前が付けられます。 例として、次の表に証明書とキーの例を示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディレクトリ名</th>
<th align="left">ファイル名</th>
<th align="left">型</th>
<th align="left">アクセス条件</th>
<th align="left">コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardid</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (R) A (RW)</td>
<td align="left">カード識別子</td>
</tr>
<tr class="even">
<td align="left">&lt;root&gt;</td>
<td align="left">cardcf</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">キャッシュファイル</td>
</tr>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardapps</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (R) A (RW)</td>
<td align="left"><p>アプリケーション名別のディレクトリインデックス。</p>
<p>詳細については、「Application Directory」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left"></td>
<td align="left">Dir</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">Base CSP/KSP アプリディレクトリ</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">cmapfile</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">CAPI GUID のインデックス</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">kxc00</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">(例) キー交換証明書0</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">ksc00</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">(例) キー署名証明書0</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">ksc01</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">(例) キー署名証明書1</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">msroots</td>
<td align="left">ファイル</td>
<td align="left">E (R) U (RW) A (RW)</td>
<td align="left">エンタープライズの信頼されたルート</td>
</tr>
</tbody>
</table>

 

**メモ**   Msroots との相互運用性: mscp \\ msroots ファイルは、PKCS \# 7 形式の証明書ストアです。

 

## <a name="span-idfile_access_controlspanspan-idfile_access_controlspanspan-idfile_access_controlspanfile-access-control"></a><span id="File_Access_Control"></span><span id="file_access_control"></span><span id="FILE_ACCESS_CONTROL"></span>ファイル Access Control


### <a name="span-idknown_principalsspanspan-idknown_principalsspanspan-idknown_principalsspanknown-principals"></a><span id="Known_Principals"></span><span id="known_principals"></span><span id="KNOWN_PRINCIPALS"></span>既知のプリンシパル

既知のプリンシパルは、何らかの方法でカードデータへのアクセスを試みることができるさまざまな種類のユーザーの識別子です。 次の表に、有効なプリンシパルと、データアクセス操作識別子と共に使用してアクセス条件を定義できる、1文字の省略形を示します。 より識別可能なプリンシパルが存在する場合もありますが、一覧は、基本 CSP/KSP とカードミニドライバー間の通信に意味を持つものに限定されます。

| 名前          | 説明                                                                                                                                                                                                                                                                                 | ニーモニック | PIN \_ ID のマッピング    |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|--------------------|
| Everyone      | 認証されていない (または匿名の) ユーザーを含む任意の要求元。                                                                                                                                                                                                                              | E        | ロールの \_ すべてのユーザー (0) |
| User          | カードのユーザークライアント。 PIN を使用してカードに id を証明します。                                                                                                                                                                                                             | U        | ロール \_ ユーザー (1)     |
| 管理者 | カードまたはカード上のデータに対する管理上の関係を持つカード発行者またはその他のパーティ。 PIN のブロック解除など、このデータを使用せずにユーザーが実行できない管理タスクを実行するために、特殊な PIN またはキー (カードまたはユーザーに対して一意ではない場合もあります) を使用します。 | A        | ロール \_ 管理者 (2)    |

 

次の説明で "everyone" を使用すると、通常は、認証されているかどうかにかかわらず、カードのすべてのユーザーを意味します。 たとえば、"すべてのユーザーがファイルを読み取ることができます" は、ユーザーまたは管理者がファイルを自動的に読み取ることができることを意味します。

ファイルシステムアクセスの場合、管理者は一般に "スーパーユーザー" と見なされ、ユーザーと同じ特権を持ちます (execute 特権を除きます)。

### <a name="span-iddirectory_access_conditionsspanspan-iddirectory_access_conditionsspanspan-iddirectory_access_conditionsspandirectory-access-conditions"></a><span id="Directory_Access_Conditions"></span><span id="directory_access_conditions"></span><span id="DIRECTORY_ACCESS_CONDITIONS"></span>ディレクトリアクセス条件

プリンシパルは、2つのアクセス許可セットを持つカードファイルシステムにディレクトリを作成できます。 次の表は、各アクセス許可の影響をまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディレクトリアクセス条件</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">UserCreateDeleteDirAc</td>
<td align="left"><p>ユーザーと管理者は、 <a href="https://docs.microsoft.com/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))"><strong>Cardcreatefile</strong></a>を使用してディレクトリにファイルを作成できます。</p>
<p>ユーザーおよび管理者は、 <a href="https://docs.microsoft.com/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468716(v=vs.85))"><strong>Carddeletedirectory</strong></a>を呼び出すことによってディレクトリを削除できます (空でない場合)。</p>
<p>すべてのユーザーは、 <a href="https://docs.microsoft.com/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468721(v=vs.85))"><strong>Cardenumfiles</strong></a>を使用して、ディレクトリの内容を一覧表示できます。</p></td>
</tr>
<tr class="even">
<td align="left">AdminCreateDeleteDirAc</td>
<td align="left"><p>管理者は、 <a href="https://docs.microsoft.com/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))"><strong>Cardcreatefile</strong></a>を使用してディレクトリにファイルを作成できます。</p>
<p>管理者は、 <a href="https://docs.microsoft.com/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468716(v=vs.85))"><strong>Carddeletedirectory</strong></a>を使用してディレクトリを削除できます。</p>
<p>すべてのユーザーは、 <a href="https://docs.microsoft.com/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468721(v=vs.85))"><strong>Cardenumfiles</strong></a>を使用して、ディレクトリの内容を一覧表示できます。</p>
<div class="alert">
<strong>メモ</strong>   この ACL は省略可能です。 スマートカードミニドライバー仕様の将来のリビジョンから削除される可能性があります。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**メモ**   ディレクトリを作成すると、すべてのユーザーに、ディレクトリ内のファイルを一覧表示するアクセス許可が自動的に付与されます。 ディレクトリに対して個別の "リスト" アクセス許可はありません。

 

### <a name="span-idfile_access_operationsspanspan-idfile_access_operationsspanspan-idfile_access_operationsspanfile-access-operations"></a><span id="File_Access_Operations"></span><span id="file_access_operations"></span><span id="FILE_ACCESS_OPERATIONS"></span>ファイルアクセス操作

プリンシパルは、さまざまな方法でファイルの内容を使用できます。 次の表に、有効な操作を示します。この一覧には、1文字の省略形と、アクセス条件を定義するためのプリンシパル指定子があります。 特に、Execute (X) は他のファイルアクセス操作と論理的な関係がないことに注意してください。これは独立した操作です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作/特権</th>
<th align="left">Description</th>
<th align="left">ニーモニック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Read</td>
<td align="left"><p>ファイルの内容を直接、または書式設定または処理された形式で受信します。</p></td>
<td align="left">R</td>
</tr>
<tr class="even">
<td align="left">Write</td>
<td align="left"><p>ファイルの内容を変更するか、ファイルを作成するか、既存のデータを削除、置換、または変更します。</p></td>
<td align="left">W</td>
</tr>
<tr class="odd">
<td align="left">実行</td>
<td align="left"><p>ファイルの内容は、要求元に代わってカードによって実行される操作に使用します。データを受信したり、feasibly によって派生させたりすることはできません。</p></td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

### <a name="span-id_file_access_conditionsspanspan-id_file_access_conditionsspanspan-id_file_access_conditionsspan-file-access-conditions"></a><span id="_File_Access_Conditions"></span><span id="_file_access_conditions"></span><span id="_FILE_ACCESS_CONDITIONS"></span>ファイルアクセス条件

アクセス条件は Acl に似ています。 アクセス条件は、特定のファイルにアクセスできるプリンシパルと実行できる操作を制御します。 カード上の各ファイルには、プリンシパルの一覧とそのアクセス特権によって記述できるアクセス条件があります。 説明にプリンシパルまたは特権が含まれていない場合は、拒否されていると見なされます。 一般に、カードにアクセス条件が適用されます。

次の表に、 [**Cardcreatefile**](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))で使用できるアクセス条件を示し、それらを適切なアクセス条件ニーモニックにマップします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ファイルアクセス条件</th>
<th align="left">実際の意味</th>
<th align="left">アクセス条件ニーモニック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">InvalidAc</td>
<td align="left"><p>ACL の取得中にエラーが発生しました。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">すべてのユーザーの Onereaduserwriteac</td>
<td align="left"><p>つまり、すべてのユーザーがファイルを読み取り、ファイル情報 (<a href="https://docs.microsoft.com/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468727(v=vs.85))"><strong>Cardreadfile</strong></a>または<strong>cardgetfileinfo</strong>) を取得できます。また、ユーザーと管理者は、ファイルの読み取り、ファイルの書き込み、およびファイルの削除を行うことができます。</p></td>
<td align="left">E (R)、U (RW)、A (RW)</td>
</tr>
<tr class="odd">
<td align="left">UserWriteExecuteAc</td>
<td align="left"><p>ユーザーはファイルを作成し、ファイルを "実行" できます。また、ファイルを削除することもできます。 ユーザーを含むユーザーは、ファイルの内容を読み取ることができません。 また、管理者はこのファイルの内容を書き込むことはできますが、実行することはできません。ファイルを削除することもできます。</p></td>
<td align="left">U (WX) A (W)</td>
</tr>
<tr class="even">
<td align="left">すべての Onereadadminwriteac</td>
<td align="left"><p>これは、すべてのユーザーがファイルを読み取り、ファイル情報 (<a href="https://docs.microsoft.com/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468727(v=vs.85))"><strong>Cardreadfile</strong></a>または<strong>cardgetfileinfo</strong>) を取得できることを意味しますが、ファイルの書き込みとファイルの削除を行うことができるのは管理者だけです。</p></td>
<td align="left">E (R)、U (R)、A (RW)</td>
</tr>
<tr class="odd">
<td align="left">UnknownAc</td>
<td align="left"><p>このファイルは、事前に定義されている AC の種類の1つではないカードのアクセス条件 (AC) によって保護されています。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">UserReadWriteAc</td>
<td align="left"><p>すべてのユーザーの読み取り/書き込み////(例: パスワードウォレットファイル)</p></td>
<td align="left">U (RW)、A (RW)</td>
</tr>
<tr class="odd">
<td align="left">AdminReadWriteAc</td>
<td align="left"><p>すべてのユーザー/ユーザーにアクセスしない</p>
<p>管理者の読み取り/書き込み</p>
<p>//</p>
<p>例: 管理データ。</p></td>
<td align="left">A (RW)</td>
</tr>
</tbody>
</table>

 

次の表に、一般的な項目のアクセス条件の例をいくつか示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アクセス条件</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">E (X) U (W) A (W)</td>
<td align="left"><p>これは、ユーザー PIN のアクセス条件になります。 ユーザーは、PIN を必要とする操作が開始されるときには認識されません。 ユーザーの id を確立するには、PIN を "実行済み" にする必要があります。 PIN を入力すると、ユーザーの id が E から U に昇格します。ユーザーと管理者の両方が PIN を書き込むことができます。</p></td>
</tr>
<tr class="even">
<td align="left">U (WX) A (W)</td>
<td align="left"><p>ユーザーの秘密キーファイルはカードから読み取ることはできません。ユーザーのみが暗号化操作にそのコンテンツを使用できます。 このデータは、ユーザーまたは管理者によって変更される可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left">E (R) U (R) A (RW)</td>
<td align="left"><p>カード識別子。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idnotes_on_the_directory_and_file_access_conditionsspanspan-idnotes_on_the_directory_and_file_access_conditionsspanspan-idnotes_on_the_directory_and_file_access_conditionsspannotes-on-the-directory-and-file-access-conditions"></a><span id="Notes_on_the_Directory_and_File_Access_Conditions"></span><span id="notes_on_the_directory_and_file_access_conditions"></span><span id="NOTES_ON_THE_DIRECTORY_AND_FILE_ACCESS_CONDITIONS"></span>ディレクトリおよびファイルアクセス条件に関する注意事項

-   プリンシパルは、 [**Cardgetfileinfo**](https://docs.microsoft.com/previous-versions/dn468727(v=vs.85))を成功させるために、ファイルに対する読み取りアクセス権を必要とします。
-   ディレクトリの内容を一覧表示するための個別のリストアクセス許可はありません。
-   "ディレクトリへのアクセスを作成する" とは、ディレクトリにファイルを作成する特権を持つことを意味します。 "ディレクトリへのアクセスを削除する" は、ディレクトリ自体を削除する特権を持っていることを意味します。 ファイルを削除するには、カードプリンシパルにファイル自体への書き込みアクセス権が必要です。
-   スマートカードミニドライバーインターフェイスを使用して、E (W) アクセス許可を持つディレクトリを作成することはできません。
-   スマートカードミニドライバーインターフェイスを使用して、ファイルまたはディレクトリを削除して再作成しなくても、ファイルまたはディレクトリのアクセス許可を変更することはできません。
-   スマートカードミニドライバーインターフェイスを使用して、管理者または認証されていないユーザーが所有する秘密キーファイルを作成することはできません。
-   スマートカードミニドライバーインターフェイスを使用してカード上にピンファイルを作成することはできません (E (X)、U (W)、および W)。
-   スマートカードミニドライバーインターフェイスを使用してディレクトリアクセス条件を照会することはできません。
-   スマートカードミニドライバーインターフェイスを使用すると、使用可能なアクセス条件の組み合わせのサブセットを使用してファイルを作成できます。

 

 





