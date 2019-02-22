---
title: DesktopAutoplayHandler
description: DesktopAutoplayHandler
ms.assetid: e1a07580-36dd-4618-b522-3f7605c9b87b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578f2071d1847814bc878de55e704875cf6f9f80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559089"
---
# <a name="desktopautoplayhandler"></a>DesktopAutoplayHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DesktopAutoplayHandler 要素には、デバイスが接続されているし、既定のアクションが設定されていないときに、推奨される自動再生操作として表示されるデスクトップ アプリを指定します。 ユーザーはデバイスをプラグインするたびに、自動再生イベントが発生します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<DesktopAutoplayHandler>
  text
</DesktopAutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


自動再生イベントを処理するデスクトップ アプリを示す文字列。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

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
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p>親要素、 <a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">WindowsInfo XML スキーマ</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="DesktopAutoplayHandler" type="xs:string" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


デスクトップ アプリを設定すると、DesktopAutoplayHandler 要素で、デスクトップの自動再生ハンドラーの文字列を指定します。 文字列は、次のレジストリ キーの下に登録されているハンドラー サブキーの名前から取得できます。

``` syntax
HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\AutoplayHandlers\Handlers
```

DesktopAutoplayHandler 要素は省略可能です。

 

 





