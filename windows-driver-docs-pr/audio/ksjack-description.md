---
title: KSJACK\_構造の説明
description: KSJACK\_説明構造体のオーディオ ジャックの物理属性を指定します。
ms.assetid: 303bc73a-fe47-499b-97b3-7c49a40e8cfa
keywords:
- KSJACK_DESCRIPTION 構造オーディオ デバイス
- PKSJACK_DESCRIPTION 構造体ポインター オーディオ デバイス
topic_type:
- apiref
api_name:
- KSJACK_DESCRIPTION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1657777c2466aa50bbbda559ea3f3bb6dd4d09e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560723"
---
# <a name="ksjackdescription-structure"></a>KSJACK\_構造の説明


KSJACK\_説明構造体のオーディオ ジャックの物理属性を指定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct {
  DWORD              ChannelMapping;
  DWORD              Color;
  EPcxConnectionType ConnectionType;
  EPcxGeoLocation    GeoLocation;
  EPcxGenLocation    GenLocation;
  EPxcPortConnection PortConnection;
  BOOL               IsConnected;
} KSJACK_DESCRIPTION, *PKSJACK_DESCRIPTION;
```

<a name="members"></a>Members
-------

**ChannelMapping**  
対応するスピーカー位置をオーディオ チャネルのマッピングを指定します。 **ChannelMapping** 、KSAUDIO のビットマスクを\_スピーカー\_*XXX*フラグ (たとえば、スピーカー\_フロント\_左 |スピーカー\_フロント\_右)、Ksmedia.h ヘッダー ファイルで定義されています。 **ChannelMapping**アナログ レンダリング ピンには 0 以外の値にする必要があります。 キャプチャの pin やデジタル レンダリング pin では、このメンバーを 0 に設定します。

&gt; \[!注\]&gt;最初に定義された Devicetopology.h **ChannelMapping**型の列挙として**EChannelMapping**します。 **EChannelMapping**列挙以降は非推奨とされているし、は、Windows Vista および Windows オペレーティング システムの以降のバージョンでは使用されなくします。

 

**色**  
Jack の色を指定します。 色は、8 ビットの青、緑、および赤のカラー コンポーネントを連結して形成される 32 ビットの RGB 値として表されます。 青のコンポーネントが 8 の最下位ビット (ビット 0 ~ 7) を占有、緑のコンポーネントは 8 ~ 15 のビットを占有および赤のコンポーネントがビット 16-23 を占有します。 8 の最上位ビットは、ゼロです。 ジャック色が不明または物理のコネクタで識別できる色はありません、このメンバーの値は黒、0x00000000 にします。

**ConnectionType**  
この回線のモジュラー ジャックの物理的な接続の種類を指定します。 このメンバーの値は、のいずれか、 **EPcxConnectionType**の次の表に示す列挙値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">コネクタの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eConnTypeUnknown</p></td>
<td align="left"><p>Unknown</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnType3Point5mm</p></td>
<td align="left"><p>3.5 mm minijack</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeQuarter</p></td>
<td align="left"><p>1/4 インチのジャック</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeAtapiInternal</p></td>
<td align="left"><p>ATAPI 内部コネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeRCA</p></td>
<td align="left"><p>RCA ジャック</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOptical</p></td>
<td align="left"><p>光のコネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeOtherDigital</p></td>
<td align="left"><p>一般的なデジタル コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOtherAnalog</p></td>
<td align="left"><p>一般的なアナログ コネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeMultichannelAnalogDIN</p></td>
<td align="left"><p>マルチ チャネルのアナログ DIN コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeXlrProfessional</p></td>
<td align="left"><p>XLR コネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeRJ11Modem</p></td>
<td align="left"><p>RJ11 モデム コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeCombination</p></td>
<td align="left"><p>コネクタの組み合わせ</p></td>
</tr>
</tbody>
</table>

 

**GeoLocation**  
ジャックの幾何学的場所です。 このメンバーの値は、のいずれか、 **EPcxGeoLocation**の次の表に示す列挙値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">ジオメトリの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGeoLocRear</p></td>
<td align="left"><p>背面</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocFront</p></td>
<td align="left"><p>前面</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocLeft</p></td>
<td align="left"><p>Left</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRight</p></td>
<td align="left"><p>右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocTop</p></td>
<td align="left"><p>Top</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocBottom</p></td>
<td align="left"><p>Bottom</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocRearPanel</p></td>
<td align="left"><p>背面のスライド オープンまたは開いているプル パネル</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRiser</p></td>
<td align="left"><p>ライザー カード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocInsideMobileLid</p></td>
<td align="left"><p>モバイル コンピューターのカバーを徹底</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocDrivebay</p></td>
<td align="left"><p>ドライブ ベイ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocHDMI</p></td>
<td align="left"><p>HDMI コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocOutsideMobileLid</p></td>
<td align="left"><p>モバイル コンピューターのカバーを外部</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocATAPI</p></td>
<td align="left"><p>ATAPI コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocNotApplicable</p></td>
<td align="left"><p>適用できません。 参照してください<strong>解説</strong>セクション。</p></td>
</tr>
</tbody>
</table>

 

**GenLocation**  
ジャックの一般的な場所を指定します。 このメンバーの値は、のいずれか、 **EPcxGenLocation**の次の表に示す列挙値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">一般的な場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGenLocPrimaryBox</p></td>
<td align="left"><p>プライマリのシャーシの</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocInternal</p></td>
<td align="left"><p>内側のプライマリ シャーシ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGenLocSeparate</p></td>
<td align="left"><p>個別のシャーシの</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocOther</p></td>
<td align="left"><p>その他の場所</p></td>
</tr>
</tbody>
</table>

 

**PortConnection**  
ジャックによって表されるポートの種類を指定します。 このメンバーの値は、のいずれか、 **EPxcPortConnection**の次の表に示す列挙値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">ポートの接続の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ePortConnJack</p></td>
<td align="left"><p>回線のモジュラー ジャック</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnIntegratedDevice</p></td>
<td align="left"><p>デバイスの統合のスロット</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ePortConnBothIntegratedAndJack</p></td>
<td align="left"><p>ジャックと統合された、デバイスのスロットの両方</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnUnknown</p></td>
<td align="left"><p>Unknown</p></td>
</tr>
</tbody>
</table>

 

**IsConnected**  
入力ジャックに接続されている外部デバイスがあるかどうかを示します。 オーディオのコント ローラーがこのピンの値のジャック検出をサポートしているか**IsConnected**ジャックが特定の時点、プラグインによって占有されているかどうかを正確に示す必要があります。 この値は常に設定する必要があります**TRUE**ジャック検出をサポートしていないデバイス。

<a name="remarks"></a>注釈
-------

この構造が使用者、 [ **KSPROPERTY\_ジャック\_説明**](ksproperty-jack-description.md) Windows Vista 以降のプロパティ。 エンドポイント デバイスとオーディオのアダプターのハードウェア デバイス間の接続の一部であるオーディオ ジャックがについて説明します。 ジャックに、エンドポイント デバイスを接続するジャックから取り外すことをユーザーに必要なときにオーディオ アプリケーションできるわかりやすい情報構造で使用ジャックを検索するのにユーザーを支援します。

オーディオ デバイスを使用してオーディオ デバイスが物理的にアクセスできるジャックを公開しない場合、 **eGeoLocNotApplicable**を Windows と Windows ベースのアプリに物理回線のモジュラー ジャックがないことを示す値。 そのため、ありません幾何学的場所か。 たとえば、オーディオ デバイスは、アクセス可能な任意のジャックせず、マザーボードに統合できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY\_ジャック\_の説明**](ksproperty-jack-description.md)

 

 






