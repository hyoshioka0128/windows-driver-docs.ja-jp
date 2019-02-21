---
title: ISDN アダプターの ISDN キーと値を指定します。
description: ISDN アダプターの ISDN キーと値を指定します。
ms.assetid: ba2156c1-fb54-4e1e-b0ec-72aa2d950505
keywords:
- 追加レジストリ セクション WDK ネットワー キング、ISDN アダプター
- ISDN アダプターの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ccf565d14e9366e84bb020a0035f4cd426f2c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548884"
---
# <a name="specifying-isdn-keys-and-values-for-an-isdn-adapter"></a>ISDN アダプターの ISDN キーと値を指定します。





加え、 **WanEndpoints**値の場合は、ISDN アダプターを追加する必要があります、INF ファイル (を通じて、*追加レジストリ セクション*) 次のキーと、アダプターのインスタンス キーの値。 詳細については、次を参照してください。 [WAN アダプター用の WAN のエンドポイントを指定する](specifying-wan-endpoints-for-a-wan-adapter.md)します。

**注**ISDN ドライバーが Windows 8.1、Windows Server 2012 R2 で非推奨とそれ以降。



-   **IsdnNumDChannels**

    ISDN アダプターでサポートされている D チャネルの数を指定します。

-   **IsdnAutoSwitchDetect** (省略可能)

    ISDN アダプターがスイッチの自動検出をサポートしているかどうかを指定します。 値 1 は、アダプターがスイッチの自動検出をサポートしていることを示します。 値 0 は、アダプターがスイッチの自動検出をサポートしていないことを示します。

-   **IsdnSwitchTypes**

    ISDN アダプターによってサポートされているスイッチの種類を指定します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Switch</th>
    <th align="left">説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_AUTO</p></td>
    <td align="left"><p>自動検出 (北米のみ)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_ATT</p></td>
    <td align="left"><p>ESS5 (AT & T、North America)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NI1</p></td>
    <td align="left"><p>National ISDN 1 (NI 1)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_NI2</p></td>
    <td align="left"><p>National ISDN 2 (NI 2)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NT1</p></td>
    <td align="left"><p>北 Telecom DMS 100 (NT 1)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_INS64</p></td>
    <td align="left"><p>NTT INS64 (日本)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_1TR6</p></td>
    <td align="left"><p>ドイツ語の National (1TR6)。 このスイッチの種類が使用されることはほとんどありません。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_VN3</p></td>
    <td align="left"><p>フランス語の National (VN3)。 このスイッチの種類が使用されることはほとんどありません。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_NET3</p></td>
    <td align="left"><p>ヨーロッパ ISDN (DSS1)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_DSS1</p></td>
    <td align="left"><p>ヨーロッパ ISDN (DSS1)</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_AUS</p></td>
    <td align="left"><p>オーストラリア国内です。 このスイッチの種類が使用されることはほとんどありません。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_BEL</p></td>
    <td align="left"><p>ベルギー National です。 このスイッチの種類が使用されることはほとんどありません。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_VN4</p></td>
    <td align="left"><p>フランス語の National (VN4)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_SWE</p></td>
    <td align="left"><p>スウェーデン語の National</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>ISDN_SWITCH_ITA</p></td>
    <td align="left"><p>National イタリア語</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>ISDN_SWITCH_TWN</p></td>
    <td align="left"><p>台湾</p></td>
    </tr>
    </tbody>
    </table>




複数のスイッチの種類を指定するには、一緒に個々 のスイッチの型の値を追加だけです。

ISDN のコンポーネントのインストール中に自動的に実行され、ISDN ウィザードでは、ユーザーによって指定されたスイッチの型のいずれかを選択**IsdnSwitchTypes**します。 選択したスイッチの種類は、ISDN ウィザードは、その後の構成に表示されます。 その他の ISDN パラメーターを決定します。 これらの ISDN パラメーターには、電話番号、SPID (サービスのプロファイルの識別子)、サブアドレス、および複数加入電話番号が含まれます。


-   **IsdnNumBChannels**値と*D チャネル*D チャネルごとにキー

    *D チャネル*キーは、0 ~ 9 D チャネルを識別する 0 から始まるインデックス。 **IsdnNumBChannels** 21\_DWORD の値に追加、 *D チャネル*キー。 **IsdnNumBChannels** B チャネル D チャネルでサポートされている数を指定します。

例を次に、*追加レジストリ セクション*ISDN アダプターのインスタンス キーに ISDN キーと値を追加します。 2 つの D チャネルは、アダプターの指定され、D チャネルごとに 2 つの B チャネルが指定されます。

```INF
[ISDNadapter.reg]
HKR,,  WanEndPoints,         0x00010001, 4
HKR,,  IsdnNumDChannels,     0x00010001, 2
HKR,,  IsdnAutoSwitchDetect, 0x00010001, 1
HKR,,  IsdnSwitchTypes,      0x00010001, 0x00000004  ;NI1

HKR, 0, IsdnNumBChannels,    0x00010001, 2

HKR, 1, IsdnNumBChannels,    0x00010001, 2
```

ISDN ウィザード自体では、ISDN キーと値も、ユーザーによって指定されたパラメーター値に基づいて、ISDN アダプターのインスタンス キーに追加します。 ISDN ウィザードは、次のキーと値を追加します。

-   **IsdnSwitchType**

    21\_ISDN アダプターのユーザーによって選択されたスイッチの種類を示す DWORD。

-   **IsdnMultiSubscriberNumbers** D チャネルごとの値

    21\_マルチ\_D チャネルに対して、ユーザーが指定されている複数加入電話番号を示す SZ 値。

-   A *B チャネル*キーと**IsdnSpid**、 **IsdnPhoneNumber**、または**IsdnSubaddress**各 B チャネルの値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">キーまたは値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>B チャネル</em>キー</p></td>
<td align="left"><p>B チャネルを識別する 0 から始まるインデックス。 最大値、 <em>B チャネル</em>キーが 1 より小さい<strong>IsdnNumBchannels</strong> B チャネルが所属する D チャネルに割り当てられた値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IsdnSpid</strong></p></td>
<td align="left"><p>B チャネルのユーザーが指定されている場合に、SPID を示す REG_SZ 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IsdnPhoneNumber</strong></p></td>
<td align="left"><p>電話番号、存在する場合、ユーザーが指定した、B チャネルにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IsdnSubaddress</strong></p></td>
<td align="left"><p>サブアドレス、存在する場合、ユーザーが指定した、B チャネルにします。</p></td>
</tr>
</tbody>
</table>



次の例では、ISDN アダプターのレジストリ セクションのレイアウトです。 各レジストリ キーは、たとえば、角かっこで囲まれました。\[ *KeyName* \]します。 ISDN キーと ISDN アダプターの INF ファイルによって追加された値は、太字のテキストで強調表示されます。ISDN キーと ISDN ウィザードによって追加された値は、通常の (nonboldface) テキストに表示されます。

```INF
[...Enum\emumeratorID\device-instance-id]  ;ISDN adapter instance key
WanEndpoints=4
IsdnNumDChannels=2
IsdnAutoSwitchDetect=1
IsdnSwitchType=0x4  ;National ISDN 1

[...Enum\emumeratorID\device-instance-id\0]  ;D-channel 0
IsdnNumBChannels=2
IsdnMultiSubscriberNumbers=1234567 2345678 3456789

[...Enum\emumeratorID\device-instance-id\0\0]  ;B-channel 0 for D-channel 0
IsdnSpid=00555121200
IsdnPhoneNumber=5551212
IsdnSubaddress=

[...Enum\emumeratorID\device-instance-id\0\1]  ;B-channel 1 key for D-channel 0
IsdnSpid=00555121300
IsdnPhoneNumber=5551213
IsdnSubaddress=

[...Enum\emumeratorID\device-instance-id\1]  ;D-channel 1 key
IsdnNumBChannels=2
IsdnMultiSubscriberNumbers=8675309 2390125 7658156

[...Enum\emumeratorID\device-instance-id\1\0]  ;B-channel 0 for D-channel 1
IsdnSpid=00555987600
IsdnPhoneNumber=5559876
IsdnSubaddress=

[...Enum\emumeratorID\device-instance-id\1\0]  ;B-channel 1 for D-channel 1
IsdnSpid=00555876500
IsdnPhoneNumber=5558765
IsdnSubaddress=
```









