---
title: .kdfiles (セット ドライバー置換 Map)
description: .Kdfiles コマンドは、ファイルを読み取り、ドライバーの置換マップとしてその内容が使用されます。
ms.assetid: 3b0ac8c1-f0bd-4878-9303-23d6999650ee
keywords:
- Set ドライバー置換マップ (.kdfiles) コマンド
- ドライバーの置換マップ、ドライバー置換マップの設定 (.kdfiles) コマンド
- .kdfiles (ドライバーの置換マップのセット) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kdfiles (Set Driver Replacement Map)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 95e85cd4e0d5bc300ec195d55d0e25d33891891c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556625"
---
# <a name="kdfiles-set-driver-replacement-map"></a>.kdfiles (セット ドライバー置換 Map)


**.Kdfiles**コマンド ファイルを読み取り、ドライバーの置換マップとしてその内容が使用されます。

```dbgcmd
.kdfiles MapFile 
.kdfiles -m OldDriver NewDriver
.kdfiles -s SaveFile 
.kdfiles -c 
.kdfiles 
```

## <a name="span-idddkmetasetdriverreplacementmapdbgspanspan-idddkmetasetdriverreplacementmapdbgspanparameters"></a><span id="ddk_meta_set_driver_replacement_map_dbg"></span><span id="DDK_META_SET_DRIVER_REPLACEMENT_MAP_DBG"></span>パラメーター


<span id="_______MapFile______"></span><span id="_______mapfile______"></span><span id="_______MAPFILE______"></span> *MapFile*   
読み取るドライバー置換マップ ファイルを指定します。

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
現在関連付けリストにドライバー交換の関連付けを追加します。

<span id="_______OldDriver______"></span><span id="_______olddriver______"></span><span id="_______OLDDRIVER______"></span> *OldDriver*   
ターゲット コンピューターで、以前のドライバのパスとファイル名を指定します。 構文は、 *OldDriver*は後の最初の行の場合と同じ**マップ**ドライバー置換ファイル。 この構文の詳細については、[ドライバー ファイルのマッピング](mapping-driver-files.md)を参照してください。

<span id="_______NewDriver______"></span><span id="_______newdriver______"></span><span id="_______NEWDRIVER______"></span> *NewDriver*   
新しいドライバーのパスとファイル名を指定します。 このドライバーは、ホスト コンピューターで、またはその他のネットワークの場所にできます。 構文は、 *NewDriver*が 2 番目の行のと同じ**マップ**ドライバー置換ファイル。 この構文の詳細については、[ドライバー ファイルのマッピング](mapping-driver-files.md)を参照してください。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
ファイルを作成し、現在のドライバーの交換の関連付けをそのファイルに書き込みます。

<span id="_______SaveFile______"></span><span id="_______savefile______"></span><span id="_______SAVEFILE______"></span> *SaveFile*   
作成するファイルの名前を指定します。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
既存のドライバー置換マップを削除します。 (このオプションは、マップ ファイル自体は変更されません。 代わりに、このオプションをクリア、デバッガーの現在のマップ設定します。)

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

使用することができます、 **.kdfiles** Microsoft Windows XP 以降のバージョンの Windows でコマンド。 以前のバージョンの Windows でこのコマンドを使用する場合、コマンドは影響を与えませんし、エラーを生成しません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x86 ベースおよび Itanium ベースのプロセッサのみ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細とドライバーの置換とカーネル モードの他のモジュールの交換の例については、ドライバーの置換マップ ファイルの形式と、この機能を使用して適用される制限事項の説明を参照してください[のドライバーファイルのマッピング](mapping-driver-files.md).

<a name="remarks"></a>注釈
-------

使用する場合、 **.kdfiles**デバッガーは、パスとドライバー交換の現在のマップ ファイルの名前と置換のアソシエーションの現在のセットが表示されます。 パラメーターを指定せずコマンド。

指定した、このコマンドを実行すると*MapFile*ファイルは読み取り専用です。 ファイルが見つからない場合、または適切な形式のテキストが含まれていない場合は、デバッガーには、「ファイルの関連付けを読み込めません」を示すメッセージが表示されます。

場合は、指定したファイルは、適切なドライバー置換マップ ファイルの形式では、デバッガーは、ファイルの内容を読み込み、ドライバーの置換のマップに使用します。 このマップは、デバッガーを終了するまで、または別に実行するまで **.kdfiles**コマンド。

ファイルが読み取られた後と、ドライバーの置換のマップをファイルへの後続の変更してに影響することはありません (これらの変更をもう 1 つ後にしない限り、 **.kdfiles**コマンド)。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP および Windows オペレーティング システムの以降のバージョンでサポートされています。</p></td>
</tr>
</tbody>
</table>

 

 





