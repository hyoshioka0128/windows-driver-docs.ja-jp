---
title: AutoplayHandler
description: AutoplayHandler
ms.assetid: 0ee7ac9b-7c1a-4267-b718-ba110ef5b12d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53a0041d692a7208998922bef0bc32ffaabacfc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556891"
---
# <a name="autoplayhandler"></a>AutoplayHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

AutoplayHandler 要素には、ユーザーはデバイスをプラグインと、推奨される自動再生操作として表示される UWP デバイス アプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<AutoplayHandler>
  child elements
</AutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="packageidentity.md" data-raw-source="[PackageIdentity](packageidentity.md)">PackageIdentity</a></p></td>
<td><p>アプリのパッケージ id (名前とパブリッシャー) を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="application-windowsinfo-v2.md" data-raw-source="[Application](application-windowsinfo-v2.md)">アプリケーション</a></p></td>
<td><p>アプリのアプリケーション ID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="verb.md" data-raw-source="[Verb](verb.md)">動詞</a></p></td>
<td><p>アプリを登録する動詞を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="autoplaytype.md" data-raw-source="[AutoplayType](autoplaytype.md)">AutoplayType</a></p></td>
<td><p>自動再生イベントがデバイス イベントまたはコンテンツのイベントであるかどうかを指定します。 自動再生では、デバイスの種類を決定し、ボリューム以外のデバイスのデバイスのイベントまたはボリュームのデバイスのコンテンツのイベントを発生させます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="enableautoplayforregisteredapps.md" data-raw-source="[EnableAutoPlayForRegisteredApps](enableautoplayforregisteredapps.md)">EnableAutoPlayForRegisteredApps</a></p></td>
<td><p>登録済みのアプリの自動再生が有効になっているかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="launchapplicationondeviceconnect.md" data-raw-source="[LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)">LaunchApplicationOnDeviceConnect</a></p></td>
<td><p>ユーザーは、デバイスをプラグインするときに、推奨される自動再生操作として表示されるアプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
      <xs:element name="AutoplayHandler" type="tns:AutoplayHandlerType" />

  <xs:complexType name="AutoplayHandlerType">
    <xs:sequence>
      <xs:element name="PackageIdentity" type="tns:PackageIdentityType" />
      <xs:element name="Application" type="tns:ApplicationType" />
      <xs:element name="Verb" type="tns:VerbType" />
      <xs:element name="AutoplayType" type="tns:AutoplayTypeType" />
      <xs:element name="EnableAutoPlayForRegisteredApps" type ="xs:boolean" default="false" minOccurs="0" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


-   構造、 [PackageIdentity](packageidentity.md)と[アプリケーション](application-windowsinfo-v2.md)要素は同じですが、アプリケーション マニフェストの構造、そのため、アプリケーションのマニフェストから要素をコピーします。

-   AutoplayHandler 要素のデバイス メタデータのほかに、指定の UWP デバイス アプリ登録する必要がありますも自動再生イベントのイベントの場合は、そのアプリケーション マニフェストで宣言を追加することで。 自動再生では、アプリの宣言を認識し、ユーザーがそのイベントに応答する実行可能なアクションの一覧で、次が含まれています。

-   表示されているパッケージのみ、 [DeviceCompanionApplications](devicecompanionapplications.md) SoftwareInfo.xml ファイル内の値は、デバイスのインストールの一部としてダウンロードされます。 場合、 [LaunchApplicationOnDeviceConnect](launchapplicationondeviceconnect.md)別のパッケージからの要素の値が、Windows にユーザーのデバイスにするは実際にかどうかがわかりません。 ユーザーのデバイスに推奨されるアプリケーションがない場合は、ユーザーは、選択では表示されません。

-   アプリケーションが同じ場合でも、 [DeviceCompanionApplications](devicecompanionapplications.md)エントリ、常にあります自動再生リストにします。 ユーザーがインターネットに接続されていないやそれ以外の場合、関連アプリケーションのダウンロードに失敗した場合、一覧には表示されません。 ただし、ユーザーは、アプリケーションが、それらが表示されます「オプション使用可能な新しい」自動再生ダイアログ ボックスで次に、デバイスを接続したとき。

AutoplayHandler 要素は省略可能です。

 

 





