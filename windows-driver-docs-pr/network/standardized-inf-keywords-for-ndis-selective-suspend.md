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


NDIS 選択的な中断をサポートする必要があります指定ミニポート ドライバーの INF ファイル、 **\*SelectiveSuspend** INF キーワードを標準化します。 管理者を更新できます、ドライバーがインストールされた後、  **\*SelectiveSuspend** でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

アダプターの **[詳細設定**] プロパティページで変更が行われた後に、ミニポートドライバーが自動的に再起動  **ことに注意**してください。

 

**\*SelectiveSuspend** INF キーワードは、キーワードを列挙します。 次の表に、考えられる INF エントリ、 **\*SelectiveSuspend** INF キーワード。 この表の列では、列挙型キーワードの次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

**注**   独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="value"></a>数値  
リスト内の各 SubkeyName に関連付けられている列挙整数値。

<a href="" id="enumdesc"></a>EnumDesc  
表示テキストで表示される各値に関連付けられている、 **詳細** プロパティ ページ。

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

 

ミニポート ドライバーを確認する必要があります、 **\*SelectiveSuspend** NDIS 選択的な中断のサポートをアドバタイズする前に、レジストリ内のキーワード値。 場合、 **\*SelectiveSuspend** キーワードが 0 の値を持つ、ミニポートがいずれかのサポートをアドバタイズする必要があります選択的な機能を中断します。 詳細については、「 [NDIS の選択的中断機能の報告](reporting-ndis-selective-suspend-capabilities.md)」を参照してください。

## <a name="ssidletimeout-inf-keyword"></a>\*SSIdleTimeout INF キーワード


NDIS 選択的な中断をサポートしていますが、省略可能な指定する必要がありますミニポート ドライバーのファイル、INF **\*SSIdleTimeout** INF キーワードを標準化します。 このキーワードは、アイドルタイムアウト時間を秒単位で指定します。 超える期間の NDIS にネットワーク アダプター上の任意のアクティビティが検出されない場合、 **\*SSIdleTimeout** 値、NDIS 開始をセレクティブ サスペンド操作を呼び出して、ミニポート ドライバーの[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数。

管理者を更新できます、ドライバーがインストールされた後、 **\*SSIdleTimeout** でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

**注**   アダプターの高度なプロパティ ページで、変更を行った後、ミニポート ドライバーが自動的に再起動します。

 

**\*SSIdleTimeout** INF キーワードは、数値 (**Int**) キーワード。 次の表に、考えられる INF エントリ、 **\*SSIdleTimeout** INF キーワード。 テーブルの列には次の属性がについて説明します、 **Int** キーワード。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があるキーワードの名前。 この名前は、ネットワークアダプターの**Ndi\\params\\** キーの下のレジストリにも表示されます。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられている表示テキスト。

**注**   独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

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

 

**注**   NDIS の値を読み取ります、 **\*SSIdleTimeout** ドライバーは、選択的 NDIS をサポートするネットワーク アダプターのすべてのインスタンスの標準化された INF キーワードを中断します。 ミニポートドライバーは、このキーワードを読み取ることはできません。

 

NDIS は、 **\*SSIdleTimeout**値の30% 以内のタイマーを使用して、アイドルタイムアウトを測定します。 たとえば場合、 **\*SSIdleTimeout** 値は 10、NDIS が最初に、アダプターがアイドル状態を検出した後、10 ~ 13 秒の間で、アダプターが中断されます。


## <a name="ssidletimeoutscreenoff-inf-keyword"></a>\*SSIdleTimeoutScreenOff INF キーワード


NDIS 選択的な中断をサポートしていますが、省略可能な指定する必要がありますミニポート ドライバーのファイル、INF **\*SSIdleTimeoutScreenOff** INF キーワードを標準化します。 このキーワードは、アイドルタイムアウト時間を秒単位で指定します。これは、画面がオフになっている場合にのみ適用されます。 超える期間の NDIS にネットワーク アダプター上の任意のアクティビティが検出されない場合、 **\*SSIdleTimeoutScreenOff** 値、画面がオフにした後、NDIS 開始をセレクティブ サスペンド操作ミニポートを呼び出すことによってドライバーの[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数。

管理者を更新できます、ドライバーがインストールされた後、 **\*SSIdleTimeoutScreenOff** でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

**メモ**  ミニポートドライバーは、アダプターの [詳細設定] プロパティページで変更が行われた後に自動的に再起動されます。

 

**\*SSIdleTimeoutScreenOff** INF キーワードは、数値 (**Int**) キーワード。 次の表に、考えられる INF エントリ、 **\*SSIdleTimeoutScreenOff** INF キーワード。 テーブルの列には次の属性がについて説明します、 **Int** キーワード。

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

 

**注**NDIS の値を読み取ります、 **\*SSIdleTimeoutScreenOff** ドライバーは、選択的 NDIS をサポートするネットワーク アダプターのすべてのインスタンスの標準化された INF キーワードを中断します。 ミニポートドライバーは、このキーワードを読み取ることはできません。

**メモ** 最大値は、テスト目的でのみ使用できます。 値が5を超える場合、HLK 認定テストは明示的にチェックして失敗します。

 
NDIS は、 **\*SSIdleTimeoutScreenOff**値の30% 以内のタイマーを使用して、アイドルタイムアウトを測定します。 たとえば場合、 **\*SSIdleTimeoutScreenOff** 値が 5 の場合、アダプターはまず NDIS では、アダプターがアイドル状態が検出された後、6.5 を 5 秒間中断されます。


 





