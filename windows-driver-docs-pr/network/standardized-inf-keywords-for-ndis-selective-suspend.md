---
title: NDIS オプションを選択するための標準化された INF キーワードを中断します。
description: NDIS オプションを選択するための標準化された INF キーワードを中断します。
ms.assetid: A45EE23D-1C60-4DA4-82A5-89DB5CE48E21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fe9ba1c7f75ea7c462996ea276a140a9e9f0175
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558148"
---
# <a name="standardized-inf-keywords-for-ndis-selective-suspend"></a>NDIS オプションを選択するための標準化された INF キーワードを中断します。


有効化、無効にするには、NDIS 選択的なが中断ミニポート ドライバーでのパラメーターを構成するは、次の標準化された INF キーワードが定義されています。

[**\*SelectiveSuspend** INF キーワード](#selectivesuspend-keyword)

[**\*SSIdleTimeout** INF キーワード](#ssidletimeout-keyword)

[**\*SSIdleTimeoutScreenOff** INF キーワード](#ssidletimeoutscreenoff-keyword)


標準化された INF キーワードの詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

## <a name="selectivesuspend-inf-keyword"></a>\*SelectiveSuspend INF キーワード


NDIS 選択的な中断をサポートする必要があります指定ミニポート ドライバーの INF ファイル、  **\*SelectiveSuspend** INF キーワードを標準化します。 管理者を更新できます、ドライバーがインストールされた後、  **\*SelectiveSuspend**でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**  ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

 

 **\*SelectiveSuspend** INF キーワードは、キーワードを列挙します。 次の表に、考えられる INF エントリ、  **\*SelectiveSuspend** INF キーワード。 このテーブルの列には、列挙型のキーワードは次の属性について説明します。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\** ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

**注**  独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="value"></a>値  
一覧で各 SubkeyName に関連付けられている列挙型の整数値。

<a href="" id="enumdesc"></a>EnumDesc  
表示テキストで表示される各値に関連付けられている、**詳細**プロパティ ページ。

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
<td align="left"><p>セレクティブ サスペンドします。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (既定)</p></td>
<td align="left"><p>有効</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーを確認する必要があります、  **\*SelectiveSuspend** NDIS 選択的な中断のサポートをアドバタイズする前に、レジストリ内のキーワード値。 場合、  **\*SelectiveSuspend**キーワードが 0 の値を持つ、ミニポートがいずれかのサポートをアドバタイズする必要があります選択的な機能を中断します。 詳細については、次を参照してください。 [Reporting NDIS セレクティブ サスペンド機能](reporting-ndis-selective-suspend-capabilities.md)します。

## <a name="ssidletimeout-inf-keyword"></a>\*SSIdleTimeout INF キーワード


NDIS 選択的な中断をサポートしていますが、省略可能な指定する必要がありますミニポート ドライバーのファイル、INF  **\*SSIdleTimeout** INF キーワードを標準化します。 このキーワードは、秒単位でアイドル状態のタイムアウト期間を指定します。 超える期間の NDIS にネットワーク アダプター上の任意のアクティビティが検出されない場合、  **\*SSIdleTimeout**値、NDIS 開始をセレクティブ サスペンド操作を呼び出して、ミニポート ドライバーの[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数。

管理者を更新できます、ドライバーがインストールされた後、  **\*SSIdleTimeout**でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**  アダプターの高度なプロパティ ページで、変更を行った後、ミニポート ドライバーが自動的に再起動します。

 

 **\*SSIdleTimeout** INF キーワードは、数値 (**Int**) キーワード。 次の表に、考えられる INF エントリ、  **\*SSIdleTimeout** INF キーワード。 テーブルの列には次の属性がについて説明します、 **Int**キーワード。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\** ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

**注**  独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="default-value"></a>既定値  
整数の既定値。

<a href="" id="minimum-value"></a>最小値  
整数値が許容される最小値。

<a href="" id="maximum-value"></a>最大値  
整数値で許可される最大値。

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
<td align="left"><p><strong>*SSIdleTimeout</strong></p></td>
<td align="left"><p>セレクティブ アイドル タイムアウトを秒単位で一時停止します。</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**注**  NDIS の値を読み取ります、  **\*SSIdleTimeout**ドライバーは、選択的 NDIS をサポートするネットワーク アダプターのすべてのインスタンスの標準化された INF キーワードを中断します。 ミニポート ドライバーは、このキーワードを読み取りません。

 

NDIS の 30% の精度はタイマーを使用して、アイドル タイムアウトを計測する、  **\*SSIdleTimeout**値。 たとえば場合、  **\*SSIdleTimeout**値は 10、NDIS が最初に、アダプターがアイドル状態を検出した後、10 ~ 13 秒の間で、アダプターが中断されます。


## <a name="ssidletimeoutscreenoff-inf-keyword"></a>\*SSIdleTimeoutScreenOff INF キーワード


NDIS 選択的な中断をサポートしていますが、省略可能な指定する必要がありますミニポート ドライバーのファイル、INF  **\*SSIdleTimeoutScreenOff** INF キーワードを標準化します。 このキーワードは、アイドル状態のタイムアウト期間を秒単位で指定しは、画面がオフの場合にのみ適用されます。 超える期間の NDIS にネットワーク アダプター上の任意のアクティビティが検出されない場合、  **\*SSIdleTimeoutScreenOff**値、画面がオフにした後、NDIS 開始をセレクティブ サスペンド操作ミニポートを呼び出すことによってドライバーの[ *MiniportIdleNotification* ](https://msdn.microsoft.com/library/windows/hardware/hh464092)ハンドラー関数。

管理者を更新できます、ドライバーがインストールされた後、  **\*SSIdleTimeoutScreenOff**でキーワード値、 **[詳細設定]** ネットワーク アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**アダプターの高度なプロパティ ページで、変更を行った後、ミニポート ドライバーが自動的に再起動します。

 

 **\*SSIdleTimeoutScreenOff** INF キーワードは、数値 (**Int**) キーワード。 次の表に、考えられる INF エントリ、  **\*SSIdleTimeoutScreenOff** INF キーワード。 テーブルの列には次の属性がについて説明します、 **Int**キーワード。

<a href="" id="subkeyname"></a>SubkeyName  
INF ファイルで指定する必要があります、キーワードの名前。 この名前は、下のレジストリにも表示されます、 **NDI\\params\\** ネットワーク アダプターのキー。

<a href="" id="paramdesc"></a>ParamDesc  
SubkeyName に関連付けられているテキスト。

**注**独立系ハードウェア ベンダー (IHV) は、SubkeyName のわかりやすいテキストを定義できます。

 

<a href="" id="default-value"></a>既定値  
整数の既定値。

<a href="" id="minimum-value"></a>最小値  
整数値が許容される最小値。

<a href="" id="maximum-value"></a>最大値  
整数値で許可される最大値。

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
<td align="left"><p><strong>*SSIdleTimeoutScreenOff</strong></p></td>
<td align="left"><p>セレクティブ アイドル タイムアウトを秒単位で一時停止します。</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**注**NDIS の値を読み取ります、  **\*SSIdleTimeoutScreenOff**ドライバーは、選択的 NDIS をサポートするネットワーク アダプターのすべてのインスタンスの標準化された INF キーワードを中断します。 ミニポート ドライバーは、このキーワードを読み取りません。

**注**最大値は、テスト目的でのみです。 HLK の認定資格試験は明示的にチェックされ、失敗値が 5 以上である場合。

 
NDIS の 30% の精度はタイマーを使用して、アイドル タイムアウトを計測する、  **\*SSIdleTimeoutScreenOff**値。 たとえば場合、  **\*SSIdleTimeoutScreenOff**値が 5 の場合、アダプターはまず NDIS では、アダプターがアイドル状態が検出された後、6.5 を 5 秒間中断されます。


 





