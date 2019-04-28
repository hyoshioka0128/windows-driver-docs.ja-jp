---
title: 検出プロセス
description: 検出プロセス
ms.assetid: 6B94CAF1-D998-4EAF-8ABB-80A21193B50F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8906f30a46eff14f77d13550247ab845328a007
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379994"
---
# <a name="discovery-process"></a>検出プロセス


Windows 7 以降、Windows ロゴ プログラム (WLP) 経由のロゴ認定を受けたのスマート カード ミニドライバーが自動的にダウンロードして Windows プラグ アンド プレイ コンポーネントがインストールされています。 Windows 7 は、PIV と互換性のあるカード クラス ミニドライバーも導入されています。 および、GID をサポートするカードのカードのエッジ。

スマート カードをリーダーに挿入されると、Windows は、次の探索プロセスを実行します。

-   スマート カードのプラグ アンド プレイ プロセス:

    このプロセスは、要求しからプラグ アンド プレイの Windows Update からロゴ認定を受けたミニドライバーをダウンロードします。

-   Winscard 探索プロセス:

    このプロセスは、互換性のあるスマート カードを PIV または GID 互換クラス ミニドライバーに関連付けます。

-   Windows スマート カード クラス ミニドライバー検出プロセスでは:

    このプロセスは、スマート カードをインストール済みのミニドライバーを関連付けます。

次の表では、さまざまな探索プロセスを使用する補助値を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ヘルパー名</th>
<th align="left">補助値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">PIV 補助</td>
<td align="left">A0 00 00 03 08 00 00 10 00 xx yy</td>
<td align="left">PIV AID: バージョン情報は含まれません。 Microsoft のスマート カード フレームワークでは、最下位 2 バイトを無視します。</td>
</tr>
<tr class="even">
<td align="left">MS GID を支援します。</td>
<td align="left">A0 00 00 03 97 42 54 46 59 xx yy</td>
<td align="left"><p>Microsoft (MS) GID AID: バージョン情報は含まれません。</p>
<p>最下位 2 バイトは、カードには送信されませんが、次のように、ホストで予約されています。</p>
<ul>
<li>これらのバイト (xx) の 1 つ目は、GID のバージョン番号の Windows スマート カード フレームワークによって使用されます。 0x01 または 0x02 GID 仕様のリビジョン番号には、このバイトを設定する必要があります。</li>
<li>2 番目のバイト (yy) は、カード アプリケーションで使用するために予約されています。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">SC PNP 補助</td>
<td align="left">A0 00 00 03 97 43 49 44 5F 01 00</td>
<td align="left">カードのプラグ アンド プレイ AID をスマートにします。</td>
</tr>
</tbody>
</table>

 

次の表では、検出プロセスによって使用されるファイルが一覧表示します。

| コマンド | 命令 (INS) 値 |
|---------|-------------------------|
| MF      | 0x3F00                  |
| EF します。ATR  | 0x2F01                  |

 

次の表は、さまざまな探索プロセスを使用するコマンドを一覧表示します。

| コマンド      | 命令 (INS) 値 |
|--------------|-------------------------|
| SELECT       | 0xA4                    |
| データを取得します。     | 0xCA                    |
| 応答を取得します。 | 0xC0                    |

 

## <a name="span-idsmartcardplugandplayprocessspanspan-idsmartcardplugandplayprocessspanspan-idsmartcardplugandplayprocessspansmart-card-plug-and-play-process"></a><span id="Smart_Card_Plug_and_Play_Process"></span><span id="smart_card_plug_and_play_process"></span><span id="SMART_CARD_PLUG_AND_PLAY_PROCESS"></span>スマート カードのプラグ アンド プレイのプロセス


プラグ アンド プレイは、互換性のある受信トレイのミニドライバーが使用できない場合に、スマート カード ミニドライバーをインストールします。 プラグ アンド プレイも更新インストールされているスマート カード ミニドライバーが Windows 更新プログラム。

これらのタスクのいずれかには、プラグ アンド プレイは、スマート カードの一意の ID を取得できる必要があります。 Windows 7 以降では、次に示しますプラグ アンド プレイを使用して、カードの一意の ID を派生するスマート カードの検出プロセス。

1.  プラグ アンド プレイでは、ATR から履歴のバイト数を取得します。 これらのバイトは、この検出プロセスで後で使用されます。
2.  プラグ アンド プレイでは、SC PNP AID を検索する SELECT コマンドを発行します。プラグ アンド プレイの問題が、独自の Windows を検索するデータの取得コマンド タグ 0x7F68 (ASN.1 DER でエンコードされた)。 詳細については、「Windows スマート カード フレームワーク カード識別子」次のサブセクションを参照してください。 このコマンドが成功した場合は、一意の識別子の一覧が返されます。 プラグ アンド プレイとしてスマート カードのデバイス ID の一覧で最初の識別子を使用し、カードの一意の ID の値を使用して 詳細については、次を参照してください。[デバイス Id](https://msdn.microsoft.com/library/windows/hardware/ff541237)します。
3.  プラグ アンド プレイ スマート カードの一意の ID に派生している場合は、手順 12. に進みます。
4.  Windows が上記の手順でデバイス ID の取得に失敗した場合、MF と EF の SELECT を発行します。ATR 後、バイナリの読み取りのコマンドでは、WU のデバイス ID として使用できる一意の識別子を取得中に Windows が成功した場合は、手順 12. に進みます。
5.  上記の手順で一意の識別子を取得するプラグ アンド プレイに失敗した場合、PIV AID の SELECT コマンドを発行します。 プラグ アンド プレイが成功すると、スマート カードの PIV と互換性のあるデバイスであると見なします。 プラグ アンド プレイでは、カードの一意の ID として、次を使用します。

    1.  デバイスの互換性のある ID として PIV と互換性のあるデバイス ID 詳細については、次を参照してください。[互換性 Id](https://msdn.microsoft.com/library/windows/hardware/ff539950)します。
    2.  デバイス ID と、カードの ATR の履歴バイト Windows で、PIV と互換性のあるデバイス id を使用して、デバイス ID と履歴 ATR のバイトがない場合は、

6.  プラグ アンド プレイ スマート カードの一意の ID に派生している場合は、手順 12. に進みます。
7.  手順 4. で SELECT コマンドが成功しなかった場合、Windows は、MS GID で SELECT コマンドを発行します。MS GID の補助選択する際にプラグ アンド プレイが成功した場合は、GID と互換性のあるデバイスをスマート カードを検討します。 プラグ アンド プレイでは、カードの一意の ID として、次を使用します。

    1.  互換性のある ID と GID と互換性のあるデバイス ID
    2.  デバイス ID と、カードの ATR の履歴バイト プラグ アンド プレイがデバイス ID と GID と互換性のあるデバイス ID を使用する履歴 ATR のバイトがない場合は、

8.  プラグ アンド プレイ スマート カードの一意の ID に派生している場合は、手順 12. に進みます。
9.  PIV AID または MS GID の支援を選択するプラグ アンド プレイに失敗した場合、カードの ATR 履歴バイト (あれば) として使用、デバイス ID のスマート カードの一意の id。
10. プラグ アンド プレイが ATR 履歴バイトを持たない場合、Windows 更新プログラムのための十分な情報がありません。 プラグ アンド プレイ s カードで検出プロセスが失敗した\_E\_予期しません。
11. プラグ アンド プレイ スマート カードの一意の ID に派生している場合は、手順 12. に進みます。
12. プラグ アンド プレイでは、検出プロセスを停止し、一意の識別子を使用します。

カードは fromWindows 8、以降はプラグ アンド プレイは、カードのドライバーを検索することがない場合、受信トレイの NULL ドライバーとペアリングされています。 カードに固有の追加のソフトウェアが必要ですし、カード、スマート カード リーダーに接続されているときの関数は、PC に接続されています。

## <a name="span-idwinscarddiscoveryprocessspanspan-idwinscarddiscoveryprocessspanspan-idwinscarddiscoveryprocessspanwinscard-discovery-process"></a><span id="Winscard_Discovery_Process"></span><span id="winscard_discovery_process"></span><span id="WINSCARD_DISCOVERY_PROCESS"></span>Winscard 検出プロセス


Winscard (Winscard.dll) 検出プロセスは、システムにインストール済みのミニドライバーのカードを関連付けるに使用されます。 プロセスの開始時に[ **SCardListCards** ](https://msdn.microsoft.com/library/windows/desktop/aa379789)または[ **SCardLocateCards** ](https://msdn.microsoft.com/library/windows/desktop/aa379794)が呼び出されます。

Windows 7 以降では、次に示します、Winscard 検出プロセス。

1.  Winscard は、Calais キー、コンピューターにインストールされているスマート カードを表すさまざまなサブキーの下のレジストリ内を検索します。 これらのサブキーにあります。

    HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\暗号化\\Calais\\スマート カード

2.  Winscard は、サブキーの ATR 値とスマート カードから取得された ATR 値間の一致のスマート カードのサブキーの下の各サブキーを検索します。 一致が見つかった場合は、手順 6 に進みます。
3.  Winscard は、ミニドライバーのスマート カードのサブキーの値と (PIV カード) の PIV デバイス ATR キャッシュまたは IDMP ATR キャッシュ (GID と互換性のあるカード) をサブキー内の値の間の一致を検索します。 一致が見つかるとステップ 6 に進みます。 場合、
4.  Winscard MS GID で SELECT コマンドを発行します。 このコマンドが成功した場合は、手順 6 に進みます。
5.  手順 4 が失敗した場合、Winscard PIV AID の SELECT コマンドを発行します。 このコマンドが成功した場合は、手順 6 に進みます。
6.  Winscard では、カードに一致するミニドライバーのレジストリ キーに対応すると、カードの名前を返します。

**注**  次の表に、Winscard 検出プロセスを使用するさまざまなレジストリ キーがについて説明します。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ キー</th>
<th align="left">使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Hkey_local_machine \software\microsoft \Cryptography\Calais\SmartCards</td>
<td align="left">Winscard は、手順 1. で Calais\SmartCards キーとしてこのキーを使用します。</td>
</tr>
<tr class="even">
<td align="left">Hkey_local_machine \ software \microsoft \Cryptography\Calais\PIV デバイス ATR キャッシュ</td>
<td align="left"><p>手順 4. で、一致が見つかった場合、一致するカードの完全な ATR は、バイナリ値として、このレジストリ キーに格納されます。 エントリの名前がランダムに選択します。</p>
<p>このエントリがキャッシュされた後は、手順 3. でパフォーマンスを向上させるために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left">Hkey_local_machine \ software \microsoft \Cryptography\Calais\IDMP ATR キャッシュ</td>
<td align="left"><p>手順 5. で一致が見つかった場合、一致するカードの完全な ATR に格納されますこのレジストリ キーをバイナリ値として。 エントリの名前がランダムに選択します。</p>
<p>このエントリがキャッシュされた後は、手順 3. でパフォーマンスを向上させるために使用されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwindowssmartcardclassminidriverdiscoveryprocessspanspan-idwindowssmartcardclassminidriverdiscoveryprocessspanspan-idwindowssmartcardclassminidriverdiscoveryprocessspan-windows-smart-card-class-minidriver-discovery-process"></a><span id="_Windows_Smart_Card_Class_Minidriver_Discovery_Process"></span><span id="_windows_smart_card_class_minidriver_discovery_process"></span><span id="_WINDOWS_SMART_CARD_CLASS_MINIDRIVER_DISCOVERY_PROCESS"></span> Windows スマート カード クラス ミニドライバー検出プロセス


Windows のスマート カード クラス ミニドライバーは、次の検出を実行します。 プロセスに[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)が呼び出されます。 ミニドライバーは、PIV または GID と互換性のあるとして関連付けられているカードをマークするには、この検出プロセスを実行します。

1.  ミニドライバーは、PIV AID の SELECT コマンドを発行します。 カードが PIV と互換性のある、検出とマークされているコマンドが成功すると、処理が終了します。
2.  それ以外の場合、ミニドライバーは、MS GID で SELECT コマンドを発行します。 コマンドが成功するか、支援の検索に失敗する場合、ミニドライバーは、MS GID としてカードをマークします。

**注:**  
-   スマート カード クラス ミニドライバーで Winscard 検出プロセスで検出された以前の場合も可能性があります応答 SELECT コマンドに、PIV または GID 補助用。 このような状況で GID のカード edge カスタム補助を実装するベンダーのカードがあります。 このようなカードでは、追加のデータ オブジェクトを Microsoft スマート カードのデータ モデルを拡張できます。
-   PIV と GID のスマート カード ベンダーは、Windows のスマート カード クラス ミニドライバーを使用し、INF のみのインストール パッケージを提供することでブランドを追加できます。 詳細については、互換性のあるカード クラス ミニドライバーを使用して、サンプルでは、INF を参照してください。[スマート カードのプラグ アンド プレイ](smart-card-plug-and-play.md)します。 プラグ アンド プレイの一致、INF に履歴バイトのみが使用されます。

    ベンダーが提供する INF ファイルは、Calais の下にエントリを作成します。\\スマート カードのレジストリ サブキーで、次の情報。

    | エントリ名                      | 種類   | Value                                     |
    |---------------------------------|--------|-------------------------------------------|
    | 80000001                        | String | Msclmd.dll                                |
    | ATR                             | バイナリ | カードの ATR                                |
    | ATRMask                         | バイナリ | カードの ATR マスク                           |
    | 暗号化プロバイダー                 | String | Microsoft Base Smart Card Crypto Provider |
    | スマート カード キー記憶域プロバイダー | String | Microsoft スマート カード キー記憶域プロバイダー |

     

 

## <a name="span-idselectionmechanismsspanspan-idselectionmechanismsspanspan-idselectionmechanismsspanselection-mechanisms"></a><span id="Selection_Mechanisms"></span><span id="selection_mechanisms"></span><span id="SELECTION_MECHANISMS"></span>選択メカニズム


### <a name="span-idapplicationsthatcontainmicrosoftidentifiersspanspan-idapplicationsthatcontainmicrosoftidentifiersspanspan-idapplicationsthatcontainmicrosoftidentifiersspanapplications-that-contain-microsoft-identifiers"></a><span id="Applications_that_Contain_Microsoft_identifiers"></span><span id="applications_that_contain_microsoft_identifiers"></span><span id="APPLICATIONS_THAT_CONTAIN_MICROSOFT_IDENTIFIERS"></span>アプリケーションを含む Microsoft 識別子

Windows スマート カード フレームワークは、Microsoft のプラグ アンド プレイ AID を使用してアプリケーションを選択しようとします。 カードが指定の支援をサポートしていない場合は、エラーを選択コマンドの後に返します。 SELECT コマンドが正常に完了すると、フレームワークは、データの取得コマンドを発行して、カードと対応するスマート カード ミニドライバーを識別しようとします。

データの取得コマンドでは、SC プラグ アンド プレイの補助がサポートされているかどうかに関係なく行われます。 これにより、アプリケーション、任意の補助に関連付けられているいずれかに関連付けられている他の資料またはありませんはこの仕様でカードの選択メカニズムを実装します。

### <a name="span-idgetdataspanspan-idgetdataspan-get-data"></a><span id="_GET_DATA"></span><span id="_get_data"></span> データを取得します。

プラグ アンド プレイ カード上の MS AID を選択した後に、スマート カード フレームワークは 0x7F68 の Windows 専用のタグを持つデータの取得コマンドを発行します。 カードは、データの取得コマンドと独自のタグをサポートする場合は、1 つまたは複数の一意の識別子の一覧を返すことで応答します。 一意の識別子は、次の「Windows スマート カード フレームワーク カード識別子」セクションで定義されている構造化する必要があります。

Windows スマート カード フレームワークは、一覧で見つけて適切なスマート カード ミニドライバーをインストールする最初の一意の識別子のみを使用します。 その他の識別子は、将来使用される可能性があります。

### <a name="span-idselectpivaidcommandspanspan-idselectpivaidcommandspanspan-idselectpivaidcommandspan-select-piv-aid-command"></a><span id="_SELECT_PIV_AID_Command"></span><span id="_select_piv_aid_command"></span><span id="_SELECT_PIV_AID_COMMAND"></span> PIV ヘルパー コマンドを選択します。

PIV アプリケーションを識別するためには、Windows は、選択 PIV ヘルパー コマンドを発行します。 このコマンドが成功すると、PIV アプリケーションは、カード上に存在してが選択されているようになりました。 このような状況では、Windows のスマート カード フレームワークは、カードのようになりました PIV 準拠のミニドライバーを関連付けます。

### <a name="span-idselectmsgidsaidcommandspanspan-idselectmsgidsaidcommandspanspan-idselectmsgidsaidcommandspan-select-ms-gids-aid-command"></a><span id="_SELECT_MS_GIDS_AID_Command"></span><span id="_select_ms_gids_aid_command"></span><span id="_SELECT_MS_GIDS_AID_COMMAND"></span> MS GID AID コマンド

MS GID アプリケーションを識別するためには、MS GID AID の選択コマンドが使用されます。 このコマンドが成功すると、MS GID アプリケーションは、カード上に存在してが選択されているようになりました。 Windows スマート カード フレームワークでは、カードと MS GID – 準拠のミニドライバーを関連付けることができました。

### <a name="span-iduseoftheatrhistoricalbytesspanspan-iduseoftheatrhistoricalbytesspanspan-iduseoftheatrhistoricalbytesspanuse-of-the-atr-historical-bytes"></a><span id="Use_of_the_ATR_Historical_Bytes"></span><span id="use_of_the_atr_historical_bytes"></span><span id="USE_OF_THE_ATR_HISTORICAL_BYTES"></span>ATR 履歴バイトの使用

次の条件では、Windows スマート カード フレームワークを ATR 履歴バイト ATR を使用して読み込むミニドライバーを決定する元に戻します。

-   スマート カードは、データの取得コマンドをサポートしていません。
-   スマート カード、支援の選択方法をこの仕様ではできません。

ATR 履歴バイトの使用は、挿入されたカードを識別するために使用される従来の方法です。 フレームワークは、ミニドライバーの検索ですべての履歴のバイトを使用します。

### <a name="span-idwindowssmartcardframeworkcardidentifierspanspan-idwindowssmartcardframeworkcardidentifierspanspan-idwindowssmartcardframeworkcardidentifierspan-windows-smart-card-framework-card-identifier"></a><span id="_Windows_Smart_Card_Framework_Card_Identifier"></span><span id="_windows_smart_card_framework_card_identifier"></span><span id="_WINDOWS_SMART_CARD_FRAMEWORK_CARD_IDENTIFIER"></span> Windows スマート カード フレームワークのカードの識別子

スマート カードは、データの取得コマンドをサポートする場合、Windows スマート カード フレームワークには、次の ASN.1 構造で書式設定されている DER TLV でエンコードされたバイト配列を返すようにするカードが期待しています。

``` syntax
CardID ::= SEQUENCE {
                   version Version DEFAULT v1,
                   vendor VENDOR,
                   guids GUIDS }

Version ::= INTEGER {v1(0), v2(1), v3(2)}
VENDOR ::= IA5STRING(SIZE(0..8))
GUID ::= OCTET STRING(SIZE(16))
GUIDS ::= SEQUENCE OF GUID
```

バージョン メンバーは、0 (v1) に設定する必要があります。

仕入先のメンバーは、"MSFT"に設定する必要があります。

GUID のメンバーは、カードとアプリケーションの組み合わせが一意に識別する 16 バイトの GUID です。 この値は、検出し、適切なスマート カード ミニドライバーの読み込みに使用されます。

**注**  IHV および ISV アプリケーションを発行するには、そのカードとアプリケーションの組み合わせの一意の GUID を作成する必要があります。

 

 

 





