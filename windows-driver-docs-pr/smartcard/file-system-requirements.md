---
title: ファイル システムの要件
description: ファイル システムの要件
ms.assetid: 2C363978-3C98-4838-8C55-F804D2C75BEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec3acad4a88463a2cc1c85cd2cd7f84a41579e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360142"
---
# <a name="file-system-requirements"></a>ファイル システムの要件


「論理」レイアウトは、Base CSP または KSP を提示されたデータ レイアウトです。 このレイアウトは、複数の人間が判読できる名前を使用しておりファイル可能性がありますと対応しません一対一、カードを使用する物理的なレイアウトでファイルを。

## <a name="span-idfilenamingrequirementsspanspan-idfilenamingrequirementsspanspan-idfilenamingrequirementsspanfile-naming-requirements"></a><span id="File_Naming_Requirements"></span><span id="file_naming_requirements"></span><span id="FILE_NAMING_REQUIREMENTS"></span>ファイルの名前付けに関する要件


ファイル名は、最大 8 つの ANSI 文字 (8 ビット)、Windows のファイルとディレクトリの名前付け規則で許可されない文字を除くで構成されます。 ディレクトリ構造は、2 つのレベルで構成されています。 ルート ディレクトリとアプリケーションで使用されるディレクトリ。 ディレクトリ名は、最大 8 つの ANSI 文字で構成されます。 ファイル名とは区別されませんディレクトリ名を生成するには、カードのミニドライバーの実装は文字列を小文字に変換する必要があります。

## <a name="span-idfilenamingvirtualizationspanspan-idfilenamingvirtualizationspanspan-idfilenamingvirtualizationspanfile-naming-virtualization"></a><span id="File_Naming_Virtualization"></span><span id="file_naming_virtualization"></span><span id="FILE_NAMING_VIRTUALIZATION"></span>ファイルの名前付けの仮想化


ディレクトリとファイルをカード上の適切な場所にマップされるカードのミニドライバーで仮想ファイル システムを実装することはできます。 カードを許可しない書き込み (National ID カード) などの通常の運用中の操作は、書き込み操作をシミュレートすることがありますが、時、カードの挿入の実行中「執筆」、およびこれらを返すことがありますすべてのファイルにファイルを維持する必要があります、読み取られます。

## <a name="span-idphysicalcarddatalayoutspanspan-idphysicalcarddatalayoutspanspan-idphysicalcarddatalayoutspan-physical-card-data-layout"></a><span id="_Physical_Card_Data_Layout"></span><span id="_physical_card_data_layout"></span><span id="_PHYSICAL_CARD_DATA_LAYOUT"></span> 物理カード データのレイアウト


次の情報カードのファイルの詳細については、カードとファイル システムの使用方法の概要です。 これらのファイルまたはその内容の知識があるカードのミニドライバーを設計することはありません。 カード ミニドライバーは、汎用化されたインターフェイス レイヤーとして記述する必要があります。

## <a name="span-idlogicaldatalayoutspanspan-idlogicaldatalayoutspanspan-idlogicaldatalayoutspanlogical-data-layout"></a><span id="Logical_Data_Layout"></span><span id="logical_data_layout"></span><span id="LOGICAL_DATA_LAYOUT"></span>論理データのレイアウト


### <a name="span-idcardidentifierspanspan-idcardidentifierspanspan-idcardidentifierspancard-identifier"></a><span id="Card_Identifier"></span><span id="card_identifier"></span><span id="CARD_IDENTIFIER"></span>カードの識別子

カード識別子は、カードの一意の識別子です。 UI では、ユーザーになんらかの形で表すことができますが、それ以外の場合は、比較に使用されるのみ参照値をカードの id を確立します。 ユーザーのカードが準備されたときに、この値が割り当てられます。 バイト配列としては構成されています。

<span id="File_Name"></span><span id="file_name"></span><span id="FILE_NAME"></span>ファイル名  
このファイルの論理名は、"CardId"です。 ルート ディレクトリになります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E(R)、U(R)、A(RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
ファイルは 16 バイトの配列として編成されます。 非透過のバイナリ データとして処理します。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
この値が割り当てられます Microsoft ソフトウェアによって確保するために、カードに対して一意の値が生成されます。 関連する可能性がありますまたは製造時に、カードに割り当てられませんが、シリアル番号はありません。

### <a name="span-idapplicationdirectoryspanspan-idapplicationdirectoryspanspan-idapplicationdirectoryspanapplication-directory"></a><span id="Application_Directory"></span><span id="application_directory"></span><span id="APPLICATION_DIRECTORY"></span>アプリケーション ディレクトリ

アプリケーション ディレクトリのファイルは、固定長のアプリケーション名のエントリの一覧で構成されます。 アプリケーションのディレクトリ名は、すべてのアプリケーションのファイルを含む論理サブディレクトリの名前です。 CAPI2 を使用するアプリケーションを名前は"mscp"インデックス値は 0 です。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>論理名  
このファイルの論理名は、"cardapps"です。 ルート ディレクトリになります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E(R)、U(RW)、A(RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
ファイルは、一連の後に 0 で終わるアプリケーション名の文字列 (ANSI) バイトのインデックスを含むレコードとして編成されます。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
アプリケーションの実装では、カードの一意のディレクトリとアプリケーションのデータ カードのキャッシュ ファイルの一意のインデックスをアプリケーション名がマップが必要です。 カードのアプリケーション ディレクトリには、アプリケーション ディレクトリの名前を検索し、これが発生する位置のインデックスを注意してください。 キャッシュ ファイルのインデックス値を検索するのにアプリケーションができるようにします。 ファイルには、アプリケーションの名前を含む 8 バイト レコードの末尾にゼロが埋められます。 アプリケーション名は、すべての 8 バイトを使用して、結果の文字列は 0 で終了する必要がないようにできます。 したがって、「作成」カードのファイルの内容は、次の 8 バイトです。

``` syntax
{‘mscp’,0,0,0,0}
```

### <a name="span-idcachefilespanspan-idcachefilespanspan-idcachefilespancache-file"></a><span id="Cache_File"></span><span id="cache_file"></span><span id="CACHE_FILE"></span>キャッシュ ファイル

パフォーマンスを向上させ、そのカードで通信を減らす、Base CSP または KSP は、さまざまな方法でカードのデータをキャッシュできます。 キャッシュ ファイルを使用するには、カード上のデータのバージョン番号を示すことにより、キャッシュのサブシステム Base CSP または KSP 内での操作を制御します。 データが変更されたときに、この値がインクリメントされます。 カードから読み取られたバージョンとキャッシュ ファイルの内部コピーを比較すると、キャッシュされたデータが使用できること、または更新する必要があるかどうかを判断する Base CSP または KSP ができます。 この判断を行う必要性を取り出して、カードを挿入し直すなど、さまざまな理由は発生します。

カードの識別子とキャッシュ ファイルをカードから読み取るには、ホスト上の時間、不確定な期間にわたってキャッシュに保存された情報を使用して許可するための十分な完全必要があります。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>論理名  
このファイルの論理名は、"CardCF"です。 ルート ディレクトリになります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E(R)、U(RW)、A(RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
ファイルでは、連続してアプリケーションを維持し、解釈するキャッシュの 32 ビット値の後に 2 バイト値の形式で編成されたグローバル データ。 これらの 1 つ目は、、Base CSP または KSP を使用する予約されています。 その後、各アプリケーションは、1 つを割り当てられる**DWORD**します。

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
アプリケーションの内部にキャッシュ データのコピーには、カードから読み取ったファイルよりも関心のあるデータの別のバージョン番号が示されている場合、アプリケーションの内部キャッシュが更新されます。 キャッシュは一般に、カードと各トランザクションの先頭にチェックされます。

アプリケーションのキャッシュ データ、キャッシュ アプリケーションごとに 1 つの Dword の配列は、アプリケーション ディレクトリのファイルからアプリケーションをインデックスによってインデックスが作成します。 アプリケーションが追加されると、ファイルは、4 バイトずつ大きくなります。

### <a name="span-idcontainermapfilespanspan-idcontainermapfilespanspan-idcontainermapfilespancontainer-map-file"></a><span id="Container_Map_File"></span><span id="container_map_file"></span><span id="CONTAINER_MAP_FILE"></span>コンテナーのマップ ファイル

コンテナーのマップ ファイルは、Base CSP または KSP によって所有されているし、CONTAINERMAPRECORD 種類のレコードの数で構成されます。 これらのレコードは、キーとそのコンテナーの証明書へのアクセスに使用できるインデックスへの CAPI によって割り当てられた GUID は通常、コンテナーの識別子を関連付けます。

ファイル内のレコードの位置 (インデックス) は、証明書とそのコンテナーに関連付けられているキーの情報のインデックスに対応します。 したがって、このようなファイル内の 2 つ目のレコードには、1 から始まるインデックスが表示されます。

このコンテナーとコンテナーのすべての署名やキーの交換キーに関連付けられている証明書は、このインデックスを共有 (UserCerts\\SignatureCert1、SignatureKey1 など)。 レコードには、コンテナーの GUID とそのインデックスに関連付けられているキーのサイズの情報が含まれます。

<span id="Logical_Name"></span><span id="logical_name"></span><span id="LOGICAL_NAME"></span>論理名  
このファイルの論理名は、"CMapFile"です。 "Mscp"ディレクトリになります。

<span id="Access_Conditions"></span><span id="access_conditions"></span><span id="ACCESS_CONDITIONS"></span>アクセス条件  
このファイルのアクセス条件は、E(R)、U(RW)、A(RW) です。

<span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容  
このファイルのアクセス条件は、E(R)、U(RW)、A(RW) です。

<span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈  
このファイルを作成し、そのコンテンツは、Base CSP または KSP を維持します。 このファイルの内部構造に関する情報は、参照のみ提供されます。 ファイル内のレコードには、次の形式があります。

**CONTAINERMAPRECORD**

これらのレコードには、CAPI によって割り当てられたコンテナーの GUID と関連付けられているキーの交換またはそのコンテナーに関連付けられているキーの署名キーのサイズが含まれます。 WORD のすべてのメンバーは、ほとんど Endean バイト順です。

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

**WszGuid** CAPI がコンテナーに割り当てられている識別子の UNICODE 文字の文字列形式のメンバーで構成されます。 通常は、必ずではありませんが、GUID 文字列です。 識別子名に特殊文字を含めることはできません"\\"。 読み取り専用のカードがプロビジョニングされると、プロビジョニング プロセスは識別子の名前のと同じガイドラインに従う必要があります。

コンテナー名が null で終わる必要がありより大きくする必要がありますできません (最大\_コンテナー\_名前\_LEN + 1) 文字の NULL ターミネータを含めた長さ。

レコードは、このテーブルから削除する必要があります、エントリは、レコードにゼロを記述することで無効になります。 このようなレコードは、新しいデータで後で上書きできます。 テーブルがありません"パック"されるアクティブでないエントリを削除します。

次のビット フラグのバイトの有効なのとおりです。

-   コンテナー レコードが有効な場合は、ビット 0 が設定されます。
-   ビット 1 は、コンテナーが既定に設定されています。 コンテナーのマップ内の 1 つのレコードは、これを持つことができます、いつでもビットを設定します。 このビットは、ビット 0 が設定されても場合にのみ設定できます。 つまり、無効な既定のコンテナーを含めることはできません。 その他のすべてのビットは、カードのミニドライバーの将来のリビジョンの現在予約されています。
-   既定のコンテナー、0x03 バイトになります。 既定ではない有効なコンテナー、この値は 0x01 です。
-   2 ~ 7 のビットは、将来使用するために予約されています。

## <a name="span-iddatalayoutsummaryspanspan-iddatalayoutsummaryspanspan-iddatalayoutsummaryspandata-layout-summary"></a><span id="Data_Layout_Summary"></span><span id="data_layout_summary"></span><span id="DATA_LAYOUT_SUMMARY"></span>データのレイアウトの概要


次の表は、カードのミニドライバーと一般的な実装の Base CSP または KSP 間のインターフェイスでのデータの組織をまとめたものです。 「論理名」は文字列ベースの CSP または KSP を使用してカードのミニドライバー; と通信するにはこれは、カードに対応する要素に直接マッピングできないこともかまいません。

証明書とキーは論理的にグループ化される Base CSP または KSP をそれぞれの目的に従ってサブディレクトリ実際のファイル名のインデックスのみを使用してに注意してください。 任意の証明書や、カードに追加されるキーは自分のディレクトリで、インデックス番号に従ってという名前です。 説明のために次の表に、いくつかの例の証明書とキーが表示されます。

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
<th align="left">種類</th>
<th align="left">アクセス条件</th>
<th align="left">コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardid</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(R) A(RW)</td>
<td align="left">カードの識別子</td>
</tr>
<tr class="even">
<td align="left">&lt;root&gt;</td>
<td align="left">cardcf</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">キャッシュ ファイル</td>
</tr>
<tr class="odd">
<td align="left">&lt;root&gt;</td>
<td align="left">cardapps</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(R) A(RW)</td>
<td align="left"><p>アプリケーションの名前でディレクトリのインデックス。</p>
<p>詳細については、' アプリケーション ディレクトリ ' を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left"></td>
<td align="left">Dir</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">基本 CSP または KSP アプリ ディレクトリ</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">cmapfile</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">インデックスへの CAPI GUID</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">kxc00</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">(例) キー交換の証明書 0</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">ksc00</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">(例) キーの署名証明書 0</td>
</tr>
<tr class="even">
<td align="left">mscp</td>
<td align="left">ksc01</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">(例) キーの署名証明書 1</td>
</tr>
<tr class="odd">
<td align="left">mscp</td>
<td align="left">msroots</td>
<td align="left">ファイル</td>
<td align="left">E(R) U(RW) A(RW)</td>
<td align="left">エンタープライズの信頼されたルート</td>
</tr>
</tbody>
</table>

 

**注**  msroots と相互運用性: mscp\\msroots ファイルは、PKCS \#7 の書式設定された証明書ストア。

 

## <a name="span-idfileaccesscontrolspanspan-idfileaccesscontrolspanspan-idfileaccesscontrolspanfile-access-control"></a><span id="File_Access_Control"></span><span id="file_access_control"></span><span id="FILE_ACCESS_CONTROL"></span>ファイルのアクセス制御


### <a name="span-idknownprincipalsspanspan-idknownprincipalsspanspan-idknownprincipalsspanknown-principals"></a><span id="Known_Principals"></span><span id="known_principals"></span><span id="KNOWN_PRINCIPALS"></span>既知のプリンシパル

既知のプリンシパルは、さまざまな種類は何らかの方法でカードのデータにアクセスしようとするユーザーの識別子です。 次の表では、アクセス条件を定義するデータ アクセス操作識別子と共に使用できる 1 つの文字の省略形で、有効なプリンシパルを示します。 特定できる複数のプリンシパルが存在することができます、一覧は、Base CSP または KSP およびカード ミニドライバーの間の通信の意味を持つものだけに制限します。

| 名前          | 説明                                                                                                                                                                                                                                                                                 | アクセラレータ キー | PIN\_ID マッピング    |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|--------------------|
| すべてのユーザー      | 要求元、ユーザーが認証されていない (または匿名) を含むです。                                                                                                                                                                                                                              | E        | ロール\_EVERYONE (0) |
| ユーザー          | カードに、PIN の使用による自身の id を提示したユーザー、カードのクライアント。                                                                                                                                                                                                             | U        | ロール\_ユーザー (1)     |
| 管理者 | カード発行者またはカードまたはカードのデータへの管理のリレーションシップを持つその他のパーティです。 特殊な暗証番号 (pin) またはキー (または可能性のあるカードまたはユーザーに一意でない可能性があります) を使用すると、暗証番号 (pin) のブロック解除など、このデータを使用せず、ユーザーが実行できない管理タスクを実行します。 | A        | ロール\_管理者 (2)    |

 

次の説明で"everyone"を使用するときに通常意味、カードのすべてのユーザー認証かどうか。 ユーザーまたは管理者は、自動的に、ファイルを読み取ることできます意味などの「ファイルをすべて読み取ることができます」。

ファイル システムへのアクセスの管理者は、一般に「スーパー ユーザー」と見なされます、(execute 権限) を除くユーザーとして、同じ権限を持ちます。

### <a name="span-iddirectoryaccessconditionsspanspan-iddirectoryaccessconditionsspanspan-iddirectoryaccessconditionsspandirectory-access-conditions"></a><span id="Directory_Access_Conditions"></span><span id="directory_access_conditions"></span><span id="DIRECTORY_ACCESS_CONDITIONS"></span>ディレクトリ アクセスの条件

プリンシパルは、2 つのアクセス許可のセットでカードのファイル システム ディレクトリを作成できます。 次の表では、各アクセス許可の効果を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ディレクトリ アクセスの状態</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">UserCreateDeleteDirAc</td>
<td align="left"><p>ユーザーと管理者にファイルを作成できます、ディレクトリを使用して<a href="https://msdn.microsoft.com/library/windows/hardware/dn468711" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468711)"> <strong>CardCreateFile</strong></a>します。</p>
<p>ユーザーと管理者は、呼び出すことで (空ではない) 場合は、ディレクトリを削除できます<a href="https://msdn.microsoft.com/library/windows/hardware/dn468716" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468716)"> <strong>CardDeleteDirectory</strong></a>します。</p>
<p>使用して、ディレクトリの内容を一覧のすべてのユーザー <a href="https://msdn.microsoft.com/library/windows/hardware/dn468721" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468721)"> <strong>CardEnumFiles</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left">AdminCreateDeleteDirAc</td>
<td align="left"><p>管理者は、ディレクトリにファイルを使用して作成できます<a href="https://msdn.microsoft.com/library/windows/hardware/dn468711" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468711)"> <strong>CardCreateFile</strong></a>します。</p>
<p>管理者を使用して、ディレクトリを削除できます<a href="https://msdn.microsoft.com/library/windows/hardware/dn468716" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468716)"> <strong>CardDeleteDirectory</strong></a>します。</p>
<p>使用して、ディレクトリの内容を一覧のすべてのユーザー <a href="https://msdn.microsoft.com/library/windows/hardware/dn468721" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468721)"> <strong>CardEnumFiles</strong></a>します。</p>
<div class="alert">
<strong>注</strong>  この ACL は省略可能です。 スマート カード ミニドライバーの仕様の将来のリビジョンから削除することがあります。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**注**  ディレクトリを作成するときにすべてのユーザー権限が自動的にディレクトリにファイルを一覧表示します。 ディレクトリに別個の"list"アクセス許可がありません。

 

### <a name="span-idfileaccessoperationsspanspan-idfileaccessoperationsspanspan-idfileaccessoperationsspanfile-access-operations"></a><span id="File_Access_Operations"></span><span id="file_access_operations"></span><span id="FILE_ACCESS_OPERATIONS"></span>ファイル アクセス操作

プリンシパルは、さまざまな方法でファイルの内容を使用できます。 有効な操作は、アクセス条件を定義するプリンシパルの指定子と共に使用できる 1 つの文字の省略形で、次の表に表示されます。 具体的には、実行 (X) に他のファイル アクセス操作への論理リレーションシップが含まれていないことに注意してください-これは独立した操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作/特権</th>
<th align="left">説明</th>
<th align="left">アクセラレータ キー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Read</td>
<td align="left"><p>ファイルの内容の直接または書式設定された、または処理された形式のいずれか。</p></td>
<td align="left">R</td>
</tr>
<tr class="even">
<td align="left">書き込み</td>
<td align="left"><p>場合によって、ファイルを作成または削除、置換、または既存のデータを変更するファイルの内容を変更します。</p></td>
<td align="left">W</td>
</tr>
<tr class="odd">
<td align="left">実行する</td>
<td align="left"><p>ファイルの内容を使用して、操作を表すために使用されるデータを受信することができなくても、要求元の代わりに、カードによって行われるまたは現実的派生させます。</p></td>
<td align="left">x</td>
</tr>
</tbody>
</table>

 

### <a name="span-idfileaccessconditionsspanspan-idfileaccessconditionsspanspan-idfileaccessconditionsspan-file-access-conditions"></a><span id="_File_Access_Conditions"></span><span id="_file_access_conditions"></span><span id="_FILE_ACCESS_CONDITIONS"></span> ファイル アクセスの条件

アクセス条件は、Acl に似ています。 特定のファイルとどのようなどのプリンシパルがアクセスできる条件コントロールへのアクセスを実行できる操作。 カード上の各ファイルには、プリンシパルとアクセス権限の一覧で説明されていることができるアクセス条件があります。 説明には、プリンシパルまたは特権が含まれていない場合を拒否すると見なされます。 一般に、アクセス条件は、カードに適用されます。

次の表に、アクセス条件で使用できる[ **CardCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/dn468711)し、適切なアクセス条件ニーモニックにマッピングします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ファイル アクセスの条件</th>
<th align="left">実際の意味</th>
<th align="left">アクセス条件のアクセラレータ キー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">InvalidAc</td>
<td align="left"><p>ACL を取得中にエラーが発生しました。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">EveryoneReadUserWriteAc</td>
<td align="left"><p>つまり、すべてのユーザー ファイルの読み取りまたは、ファイル情報を取得 (<a href="https://msdn.microsoft.com/library/windows/hardware/dn468727" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468727)"><strong>CardReadFile</strong> </a>または<strong>CardGetFileInfo</strong>)、それぞれ、およびユーザーと管理者のことができますファイルを読み取って、ファイルを書き込むファイルを削除します。</p></td>
<td align="left">E(R)、U(RW)、A(RW)</td>
</tr>
<tr class="odd">
<td align="left">UserWriteExecuteAc</td>
<td align="left"><p>ユーザーは、ファイルを書き込むことができますできます「実行」、ファイル、およびファイルを削除できます。 ファイルの内容を読み取るだれ、ユーザーを含むことができます。 管理者が記述してが実行されません、このファイルの内容は、ファイルを削除します。</p></td>
<td align="left">U(WX) A(W)</td>
</tr>
<tr class="even">
<td align="left">EveryoneReadAdminWriteAc</td>
<td align="left"><p>つまり、すべてのユーザー ファイルの読み取りまたは、ファイル情報を取得 (<a href="https://msdn.microsoft.com/library/windows/hardware/dn468727" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn468727)"><strong>CardReadFile</strong> </a>または<strong>CardGetFileInfo</strong>) をそれぞれが、その管理者だけが書き込むことができますファイルとファイルを削除します。</p></td>
<td align="left">E(R)、U(R)、A(RW)</td>
</tr>
<tr class="odd">
<td align="left">UnknownAc</td>
<td align="left"><p>ファイルは、定義済みの AC 型ではないカードにアクセス条件 (AC) によって保護されます。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">UserReadWriteAc</td>
<td align="left"><p>すべてのユーザー アクセスなし//ユーザーの読み取り書き込み////例。ウォレットのパスワード ファイル</p></td>
<td align="left">U(RW)、A(RW)</td>
</tr>
<tr class="odd">
<td align="left">AdminReadWriteAc</td>
<td align="left"><p>すべてのユーザー/ユーザーのアクセスなし</p>
<p>管理者は、読み書き</p>
<p>//</p>
<p>例:管理データ。</p></td>
<td align="left">A(RW)</td>
</tr>
</tbody>
</table>

 

次の表では、一般的な項目のいくつかのサンプルへのアクセス条件を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アクセス条件</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">E(X) U(W) A(W)</td>
<td align="left"><p>ユーザー暗証番号 (pin) のアクセス条件になります。 PIN を必要とする操作の開始時に、ユーザーは識別ではありません。 PIN 必要があります「実行」、ユーザーの id を確立します。 PIN のエントリの後、ユーザーの id E からに昇格 u です。ユーザーと管理者は、PIN を書き込む場合があります。</p></td>
</tr>
<tr class="even">
<td align="left">U(WX) A(W)</td>
<td align="left"><p>カードからユーザーの秘密キー ファイルを読み取ることがない可能性がありますでき、ユーザーのみが暗号化操作でその内容を使用できます。 このデータは、ユーザーまたは管理者によって変更可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left">E(R) U(R) A(RW)</td>
<td align="left"><p>カードの識別子です。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idnotesonthedirectoryandfileaccessconditionsspanspan-idnotesonthedirectoryandfileaccessconditionsspanspan-idnotesonthedirectoryandfileaccessconditionsspannotes-on-the-directory-and-file-access-conditions"></a><span id="Notes_on_the_Directory_and_File_Access_Conditions"></span><span id="notes_on_the_directory_and_file_access_conditions"></span><span id="NOTES_ON_THE_DIRECTORY_AND_FILE_ACCESS_CONDITIONS"></span>ディレクトリおよびファイル アクセスの条件に関する注意事項

-   プリンシパルには、ファイルに対して読み取りアクセス権が必要がある[ **CardGetFileInfo** ](https://msdn.microsoft.com/library/windows/hardware/dn468727)が成功します。
-   ディレクトリの内容を一覧表示するための独立したリストの権限はありません。
-   ディレクトリへのアクセスを「ディレクトリのアクセスを作成する」の意味は、ディレクトリにファイルを作成するための権限を持つ"delete"は、ディレクトリ自体を削除する権限を持つを意味します。 ファイルを削除するには、プリンシパルのカードは書き込みアクセス権をファイル自体が必要です。
-   E(W) アクセス許可を持つディレクトリを作成するスマート カード ミニドライバー インターフェイスを通じてことはできません。
-   スマート カード ミニドライバー インターフェイスを削除して再作成したファイルまたはディレクトリのファイルまたはディレクトリのアクセス許可を変更することはできません。
-   場合によっては、いずれかで、管理者が所有する秘密キー ファイルを作成するスマート カード ミニドライバー インターフェイスを使用またはユーザーが認証されていないことはできません。
-   スマート カード ミニドライバー インターフェイス (E(X)、U(W)、および A(W)) カードの暗証番号 (pin) ファイルを作成することはできません。
-   ディレクトリ アクセスの条件をクエリするスマート カード ミニドライバー インターフェイスを通じてことはできません。
-   のみ、使用可能な条件の組み合わせ、アクセスのサブセットを含むファイルを作成するスマート カード ミニドライバー インターフェイスを使用可能です。

 

 





