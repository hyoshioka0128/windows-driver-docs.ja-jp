---
title: 詳細プロパティ ページの構成パラメーターを指定します。
description: 高度なプロパティ ページの構成パラメーターの指定
ms.assetid: 9c243edb-f667-4244-8de2-8335fac43220
keywords:
- ネットワークの追加レジストリ セクション WDK、高度なプロパティ ページの構成
- 高度なプロパティ ページの WDK ネットワークの構成
- パラメーターの WDK ネットワーク
- 構成パラメーターの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23871adec26ce24496924927c391ed62cdeebdce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528969"
---
# <a name="specifying-configuration-parameters-for-the-advanced-properties-page"></a>高度なプロパティ ページの構成パラメーターの指定

> [!NOTE]
> Windows 10 バージョン 1703 では、前にドライバーをアップグレードし、Windows 更新プログラム、可能性があります変更で以前に定義、ドライバーの INF 値を**詳細**プロパティ ページ。
> これらの更新プログラムを Windows 10 バージョン 1703 以降の INF ファイルで、ドライバーを指定する高度なプロパティが保持されます。



Net のコンポーネント (アダプター) をインストールする INF ファイルに表示するためのアダプター構成パラメーターを指定できます、**詳細**コンポーネントのプロパティ ページ。 内のユーザーによって指定された構成値、**詳細**プロパティ ページは、コンポーネントのルート インスタンス キーに書き込まれます。

アダプターがサポートしている場合、 **[詳細設定]** プロパティ ページで、**特性**内のエントリ、 *DDInstall* NCFを含める必要があります、アダプターについて\_HAS\_UI 値。

ネットワーク INF ファイルを使用して高度なページで表示の構成パラメーターを指定します、*追加レジストリ セクション*によって参照される、 *DDInstall*コンポーネントのセクション。 このような*追加レジストリ セクション*を 1 つまたは複数の構成のサブキーを追加、 **Ndi\\params**キー。 構成パラメーターのサブキーの形式は**Ndi\\params\\**<em>SubKeyName</em>ここで、 *SubKeyName* 21\_SZベンダー固有のパラメーター名を指定する値。 たとえば、トランシーバーの種類を指定するパラメーターのキーを名前でした**Ndi\\params\\TransceiverType**します。

次のキーワードは予約されており、としては使用できません、 **Ndi\\params\\**<em>SubKeyName</em>:**BundleId**、 **BusType**、**特性**、 **ComponentId**、**説明**、 **DeviceInstanceId**、 **DriverDate**、 **DriverDesc**、 **DriverVersion**、 **InfPath**、 **InfSection**、 **InfSectionExt**、* * *IfType** **InstallTimeStamp**、**製造元**、* * *MediaType*<em>、**NetCfgInstanceId</em>*、**NetLuidIndex*<em>、</em>*  *PhysicalMediaType*<em>、* * プロバイダー</em><em>、および **ProviderName</em>* します。

追加されるパラメーターの各サブキーの**Ndi\\params**、*追加レジストリ セクション*追加する必要があります**ParamDesc**(パラメーターの説明) と**型**値。 *追加レジストリ セクション*も追加できます**既定**と **(省略可能)** パラメーターの値と、パラメーターが数値の場合**Min**、**最大**、および**手順**値。 次の表に、それぞれに追加できる値**Ndi\\params**キー。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名前</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ParamDesc</p></td>
<td align="left"><p><em>文字列</em></p></td>
<td align="left"><p>パラメーターに表示される名前、<strong>詳細</strong>ページ</p></td>
</tr>
<tr class="even">
<td align="left"><p>種類</p></td>
<td align="left"><p><strong>int</strong>、<strong>長い</strong>、 <strong>Word</strong>、 <strong>dword</strong>、<strong>編集</strong>、または<strong>列挙型</strong></p></td>
<td align="left"><p>パラメーターの型: <strong>int</strong>、<strong>長い</strong>、 <strong>Word</strong>、および<strong>dword</strong> ; 数値パラメーターの指定<strong>編集</strong>と<strong>enum</strong>テキスト パラメーターを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Default</p></td>
<td align="left"><p><em>既定値</em></p></td>
<td align="left"><p>パラメーターの既定値: 数値のパラメーターに数値を指定する必要があります ( <strong>int</strong>、<strong>長い</strong>、 <strong>Word</strong>、または<strong>dword</strong>) と一致します。指定されたパラメーターの型。文字列パラメーターの場合は、文字列である必要があります。 既定値は、必須のパラメーターに指定する必要があります。 既定値は、省略可能なパラメーターも指定できます。 ユーザーは、オプションのパラメーターの値を入力するオプションを選択するときに既定値は指定するに表示されますそのパラメーターの編集ボックス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><strong>0</strong>または<strong>1</strong></p></td>
<td align="left"><p></p>
<strong>0</strong>必要です。 パラメーターの値を指定するか、既定値を使用します。
<strong>1</strong>省略可能です。 マークできる<strong>存在しない</strong>上、 <strong>[詳細設定]</strong>ページ。</td>
</tr>
<tr class="odd">
<td align="left"><p>最小</p></td>
<td align="left"><p><em>数値</em></p></td>
<td align="left"><p>数値パラメーターの最小値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>最大</p></td>
<td align="left"><p><em>数値</em></p></td>
<td align="left"><p>数値パラメーターの最大値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>手順</p></td>
<td align="left"><p><em>数値</em></p></td>
<td align="left"><p>数値パラメーターの有効な値の間での手順 (間隔) です。 最小値は、開始点です。</p></td>
</tr>
</tbody>
</table>

 

値の範囲、**列挙型**を次の形式を持つサブキーでパラメーターが指定されます。

**Ndi\\params\\**<em>SubKeyName</em>**\\列挙型**

各列挙値には、サブキーをいる必要があります。 各**enum**サブキーは、数値 (最初の列挙値の 0 から開始) とその値の説明を指定します。

例を次に、*追加レジストリ セクション*という名前の構成パラメーターを追加する**TransType**します。

```INF
[a1.params.reg]
HKR, Ndi\params\TransType,      ParamDesc, 0, "Transceiver Type"
HKR, Ndi\params\TransType,      Type,      0, "enum"
HKR, Ndi\params\TransType,      Default,   0, "0"
HKR, Ndi\params\TransType,      Optional,  0, "0"
HKR, Ndi\params\TransType\enum, "0",       0, "Auto-Connector"
HKR, Ndi\params\TransType\enum, "1",       0, "Thick Net(AUI/DIX)"
HKR, Ndi\params\TransType\enum, "2",       0, "Thin Net (BNC/COAX)"
HKR, Ndi\params\TransType\enum, "3",       0, "Twisted-Pair (TPE)"
```

 

 





