---
title: KSJACK \_ DESCRIPTION 構造体
description: KSJACK \_ DESCRIPTION 構造体は、オーディオジャックの物理属性を指定します。
ms.assetid: 303bc73a-fe47-499b-97b3-7c49a40e8cfa
keywords:
- KSJACK_DESCRIPTION 構造のオーディオデバイス
- PKSJACK_DESCRIPTION 構造体ポインターオーディオデバイス
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
ms.openlocfilehash: d49ffc3703165d9e77cbf87a53a68007a112bc50
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851580"
---
# <a name="ksjack_description-structure"></a>KSJACK \_ DESCRIPTION 構造体


KSJACK \_ DESCRIPTION 構造体は、オーディオジャックの物理属性を指定します。

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

<a name="members"></a>メンバー
-------

**ChannelMapping**  
オーディオチャンネルの対応するスピーカーの位置へのマッピングを指定します。 **Channelmapping**は、ksk オーディオスピーカー XXX フラグのビットマスクです \_ \_ *XXX* (たとえば、スピーカーの \_ フロント \_ 左 |スピーカーの \_ フロント \_ 右)。これは、ヘッダーファイル ksmedia. h で定義されています。 **Channelmapping**は、アナログレンダリングの pin の場合にのみ0以外にする必要があります。 キャプチャピンまたはデジタルレンダリングの pin の場合は、このメンバーを0に設定します。

> [!NOTE]
> Devicetopology. h は、元々、 **EChannelMapping**型の列挙体として**channelmapping**を定義していました。 **EChannelMapping**列挙体は、非推奨とされたため、windows Vista 以降のバージョンの windows オペレーティングシステムでは使用されなくなりました。

 

**色**  
ジャックの色を指定します。 色は、8ビットの青、緑、および赤のカラー成分を連結して形成される32ビットの RGB 値として表現されます。 Blue コンポーネントは、最下位8ビット (ビット 0-7) を占有し、緑のコンポーネントはビット8-15 を占有し、赤のコンポーネントはビット16-23 を占有します。 最上位8ビットは0です。 ジャックの色が不明な場合、または物理コネクタの色が特定できない場合、このメンバーの値は0x00000000 になります。これは、黒を表します。

**ConnectionType**  
このジャックの物理接続の種類を指定します。 このメンバーの値は、次の表に示す**Epcxconnectiontype**列挙値のいずれかです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">コネクタの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eConnTypeUnknown</p></td>
<td align="left"><p>不明</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnType3Point5mm</p></td>
<td align="left"><p>3.5 mm ミニジャック</p></td>
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
<td align="left"><p>光学式コネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeOtherDigital</p></td>
<td align="left"><p>汎用デジタルコネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeOtherAnalog</p></td>
<td align="left"><p>汎用アナログコネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeMultichannelAnalogDIN</p></td>
<td align="left"><p>マルチチャネルアナログ DIN コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeXlrProfessional</p></td>
<td align="left"><p>XLR コネクタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eConnTypeRJ11Modem</p></td>
<td align="left"><p>RJ11 モデムコネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eConnTypeCombination</p></td>
<td align="left"><p>コネクタの組み合わせ</p></td>
</tr>
</tbody>
</table>

 

**情報**  
ジャックのジオメトリック位置。 このメンバーの値は、次の表に示す**Epcxgeolocation 位置**情報列挙値のいずれかです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">ジオメトリック位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGeoLocRear</p></td>
<td align="left"><p>Rear</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocFront</p></td>
<td align="left"><p>Front</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocLeft</p></td>
<td align="left"><p>左</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRight</p></td>
<td align="left"><p>権限</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocTop</p></td>
<td align="left"><p>上</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocBottom</p></td>
<td align="left"><p>下</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocRearPanel</p></td>
<td align="left"><p>背面スライド-開く、またはプルオープンパネル</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocRiser</p></td>
<td align="left"><p>ライザーカード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocInsideMobileLid</p></td>
<td align="left"><p>モバイルコンピューターのカバー内</p></td>
</tr>
<tr class="even">
<td align="left"><p>Egeolocドライブベイ</p></td>
<td align="left"><p>ドライブベイ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocHDMI</p></td>
<td align="left"><p>HDMI コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocOutsideMobileLid</p></td>
<td align="left"><p>モバイルコンピューターの外部にある</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGeoLocATAPI</p></td>
<td align="left"><p>ATAPI コネクタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGeoLocNotApplicable</p></td>
<td align="left"><p>適用不可。 「<strong>解説</strong>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

**GenLocation**  
ジャックの一般的な場所を指定します。 このメンバーの値は、次の表に示す**Epcxgenlocation**列挙値のいずれかです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">一般的な場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>eGenLocPrimaryBox</p></td>
<td align="left"><p>プライマリシャーシ</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocInternal</p></td>
<td align="left"><p>プライマリシャーシ内</p></td>
</tr>
<tr class="odd">
<td align="left"><p>eGenLocSeparate</p></td>
<td align="left"><p>別のシャーシに</p></td>
</tr>
<tr class="even">
<td align="left"><p>eGenLocOther</p></td>
<td align="left"><p>その他の場所</p></td>
</tr>
</tbody>
</table>

 

**PortConnection**  
ジャックによって表されるポートの種類を指定します。 このメンバーの値は、次の表に示す**EPxcPortConnection**列挙値のいずれかになります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">ポートの接続の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ePortConnJack</p></td>
<td align="left"><p>ブラック</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnIntegratedDevice</p></td>
<td align="left"><p>統合デバイスのスロット</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Eportconnated/Jack</p></td>
<td align="left"><p>統合デバイスのジャックとスロットの両方</p></td>
</tr>
<tr class="even">
<td align="left"><p>ePortConnUnknown</p></td>
<td align="left"><p>不明</p></td>
</tr>
</tbody>
</table>

 

**IsConnected**  
ジャックに接続されている外部デバイスがあるかどうかを示します。 オーディオコントローラーがこの pin のジャック検出をサポートしている場合、 **IsConnected**の値は、特定の時点のプラグによってそのジャックが占有されているかどうかを正確に示す必要があります。 この値は、ジャック検出をサポートしていないデバイスに対して常に**TRUE**に設定する必要があります。

<a name="remarks"></a>コメント
-------

この構造体は、Windows Vista 以降の[**Ksk プロパティ \_ ジャックの \_ 説明**](ksproperty-jack-description.md)プロパティによって使用されます。 ここでは、オーディオアダプターのエンドポイントデバイスとハードウェアデバイスとの接続の一部であるオーディオジャックについて説明します。 ユーザーがエンドポイントデバイスをジャックに接続したり、ジャックから取り外したりする必要がある場合、オーディオアプリケーションは構造内の説明情報を使用して、ユーザーがジャックを見つけやすくすることができます。

オーディオデバイスが物理的にアクセス可能なジャックを公開しない場合、オーディオデバイスは**Egeolocnotapplicable 可能**な値を使用して、Windows と windows ベースのアプリに物理ジャックがないことを示します。 そのため、幾何学的な場所はありません。 たとえば、オーディオデバイスは、アクセス可能なジャックを使用せずに、マザーボードに統合できます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSK プロパティ \_ ジャックの \_ 説明**](ksproperty-jack-description.md)

 

 






