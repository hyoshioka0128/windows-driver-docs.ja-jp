---
title: NDIS セレクティブ サスペンド用の標準化された INF キーワード
description: NDIS セレクティブ サスペンド用の標準化された INF キーワード
ms.assetid: A45EE23D-1C60-4DA4-82A5-89DB5CE48E21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdbfd229e0e8c21ed554fdd8b240baf8e9d96b9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841848"
---
# <a name="standardized-inf-keywords-for-ndis-selective-suspend"></a>NDIS セレクティブ サスペンド用の標準化された INF キーワード


次の標準化された INF キーワードは、ミニポートドライバーで NDIS セレクティブサスペンドのパラメーターを有効化、無効化、および構成するために定義されています。

[ **\*SelectiveSuspend**INF キーワード](#selectivesuspend-inf-keyword)

[ **\*SSIdleTimeout**INF キーワード](#ssidletimeout-inf-keyword)

[ **\*SSIdleTimeoutScreenOff**INF キーワード](#ssidletimeoutscreenoff-inf-keyword)


標準化された INF キーワードの詳細については、「[ネットワークデバイスの標準化](standardized-inf-keywords-for-network-devices.md)された inf キーワード」を参照してください。

## <a name="selectivesuspend-inf-keyword"></a>\*SelectiveSuspend INF キーワード


NDIS セレクティブサスペンドをサポートするミニポートドライバーの INF ファイルでは、 **\*SelectiveSuspend**標準化された INF キーワードを指定する必要があります。 ドライバーがインストールされた後、管理者は、ネットワークアダプターの **[詳細設定**] プロパティページで **\*SelectiveSuspend**キーワードの値を更新できます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

アダプターの **[詳細設定**] プロパティページで変更が行われた後に、ミニポートドライバーが自動的に再起動  **ことに注意**してください。

 

**\*SelectiveSuspend** INF キーワードは列挙キーワードです。 次の表では、 **\*SelectiveSuspend** inf キーワードに使用できる inf エントリについて説明します。 この表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

独立系ハードウェアベンダー (IHV) では、SubkeyName の説明文を定義できる  に**注意**してください。

 

<a href="" id="value"></a>数値  
リスト内の各 SubkeyName に関連付けられている列挙整数値。

<a href="" id="enumdesc"></a>EnumDesc  
**詳細**プロパティページに表示される各値に関連付けられている表示テキスト。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">Value</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*SelectiveSuspend</strong></p></td>
<td align="left"><p>選択的中断</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定値)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

ミニポートドライバーは、NDIS のセレクティブサスペンドのサポートをアドバタイズする前に、レジストリの **\*SelectiveSuspend**キーワードの値を確認する必要があります。 **\*SelectiveSuspend**キーワードの値が0の場合、ミニポートは、選択的中断機能のサポートをアドバタイズすることはできません。 詳細については、「 [NDIS の選択的中断機能の報告](reporting-ndis-selective-suspend-capabilities.md)」を参照してください。

## <a name="ssidletimeout-inf-keyword"></a>\*SSIdleTimeout INF キーワード


NDIS セレクティブサスペンドをサポートするミニポートドライバーの INF ファイルでは、省略可能な **\*SSIdleTimeout**標準化された inf キーワードを指定する必要があります。 このキーワードは、アイドルタイムアウト時間を秒単位で指定します。 NDIS が **\*SSIdleTimeout**値を超えた期間にわたってネットワークアダプターのアクティビティを検出しなかった場合、ndis はミニポートドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数を呼び出すことによって、セレクティブサスペンド操作を開始します。

ドライバーがインストールされた後、管理者は、ネットワークアダプターの **[詳細設定**] プロパティページで **\*SSIdleTimeout**キーワードの値を更新できます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

アダプターの [詳細設定] プロパティページで変更が行われた後に、ミニポートドライバーが自動的に再起動  **ことに注意**してください。

 

**\*SSIdleTimeout** INF キーワードは Numeric (**Int**) キーワードです。 次の表では、 **\*SSIdleTimeout** inf キーワードに使用できる inf エントリについて説明します。 表の列では、 **Int**キーワードの次の属性について説明しています。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

独立系ハードウェアベンダー (IHV) では、SubkeyName の説明文を定義できる  に**注意**してください。

 

<a href="" id="default-value"></a>既定値  
整数の既定値。

<a href="" id="minimum-value"></a>最小値  
整数に使用できる最小値。

<a href="" id="maximum-value"></a>最大値  
整数に使用できる最大値。

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
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">既定値</th>
<th align="left">最小値</th>
<th align="left">最大値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>* SSIdleTimeout</strong></p></td>
<td align="left"><p>選択的中断アイドルタイムアウト (秒単位)</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**  ndis**は、ドライバーが ndis セレクティブサスペンドをサポートしているネットワークアダプターのすべてのインスタンスに対して、 **\*SSIdleTimeout**標準化された INF キーワードの値を読み取ります。 ミニポートドライバーは、このキーワードを読み取ることはできません。

 

NDIS は、 **\*SSIdleTimeout**値の30% 以内のタイマーを使用して、アイドルタイムアウトを測定します。 たとえば、 **\*SSIdleTimeout**値が10の場合、アダプターがアイドル状態であることを NDIS が最初に検出した後、アダプターは 10 ~ 13 秒間中断されます。


## <a name="ssidletimeoutscreenoff-inf-keyword"></a>\*SSIdleTimeoutScreenOff INF キーワード


NDIS セレクティブサスペンドをサポートするミニポートドライバーの INF ファイルでは、省略可能な **\*SSIdleTimeoutScreenOff**標準化された inf キーワードを指定する必要があります。 このキーワードは、アイドルタイムアウト時間を秒単位で指定します。これは、画面がオフになっている場合にのみ適用されます。 画面がオフになった後に、NDIS が **\*SSIdleTimeoutScreenOff**の値を超えた期間にわたってネットワークアダプターのアクティビティを検出しなかった場合、ndis はミニポートドライバーの[*を呼び出して、セレクティブサスペンド操作を開始します。MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) handler 関数。

ドライバーがインストールされた後、管理者は、ネットワークアダプターの **[詳細設定**] プロパティページで **\*SSIdleTimeoutScreenOff**キーワード値を更新できます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

**メモ**  ミニポートドライバーは、アダプターの [詳細設定] プロパティページで変更が行われた後に自動的に再起動されます。

 

**\*SSIdleTimeoutScreenOff** INF キーワードは Numeric (**Int**) キーワードです。 次の表では、 **\*SSIdleTimeoutScreenOff** inf キーワードに使用できる inf エントリについて説明します。 表の列では、 **Int**キーワードの次の属性について説明しています。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

**メモ** 独立系ハードウェアベンダー (IHV) は、SubkeyName の説明文を定義できます。

 

<a href="" id="default-value"></a>既定値  
整数の既定値。

<a href="" id="minimum-value"></a>最小値  
整数に使用できる最小値。

<a href="" id="maximum-value"></a>最大値  
整数に使用できる最大値。

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
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">既定値</th>
<th align="left">最小値</th>
<th align="left">最大値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>* SSIdleTimeoutScreenOff</strong></p></td>
<td align="left"><p>選択的中断アイドルタイムアウト (秒単位)</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**メモ** NDIS は、ドライバーが NDIS セレクティブサスペンドをサポートしているネットワークアダプターのすべてのインスタンスに対して、 **\*SSIdleTimeoutScreenOff**標準化された INF キーワードの値を読み取ります。 ミニポートドライバーは、このキーワードを読み取ることはできません。

**メモ** 最大値は、テスト目的でのみ使用できます。 値が5を超える場合、HLK 認定テストは明示的にチェックして失敗します。

 
NDIS は、 **\*SSIdleTimeoutScreenOff**値の30% 以内のタイマーを使用して、アイドルタイムアウトを測定します。 たとえば、 **\*SSIdleTimeoutScreenOff**の値が5の場合、アダプターがアイドル状態であることを NDIS が最初に検出した後、アダプターは 5 ~ 6.5 秒間中断されます。


 





