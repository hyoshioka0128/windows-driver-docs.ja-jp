---
title: 独自の 802.1X セキュリティ メソッドの UI の拡張
description: 独自の 802.1X セキュリティ メソッドの UI の拡張
ms.assetid: 3307179f-f30b-4234-a64d-4e771ac8673e
keywords:
- 独自の 802.1 X セキュリティ WDK IHV UI 拡張機能の DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0bffd10830fa26ec8e4cd31437a3d3b91143f48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386240"
---
# <a name="extending-the-ui-for-proprietary-8021x-security-methods"></a>独自の 802.1X セキュリティ メソッドの UI の拡張




 

802.11 IHV 拡張 DLL をネイティブ サポートする独自の 802.1 X ベースのセキュリティの拡張、802.11 IHV UI 拡張機能のネイティブ DLL は、ネットワーク構成ユーザー インターフェイス (UI) を拡張できる場合**セキュリティ** タブのユーザーを許可するにはこれらの構成の拡張機能。 802.11 802.1 X のネイティブ モジュールを拡張する方法の詳細については、次を参照してください。[インターフェイス ネイティブ 802.11 802.1 X モジュール](interface-to-the-native-802-11-802-1x-module.md)します。

ネットワークの構成 UI やその他のネイティブの 802.11 コンポーネントに関する詳細については、次を参照してください。[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)します。

表示にする前に、**セキュリティ** タブで、オペレーティング システムは次の処理します。

1.  呼び出すことによって、セキュリティ プロパティの拡張機能に対してネイティブ 802.11 IHV UI 拡張 DLL のクエリ、 [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)メソッド。 オペレーティング システムの値を渡す**DOT11\_EXT\_UI\_KEYEXTENSION**メソッドの*ExtType*パラメーター。

    型のプロパティの拡張機能**DOT11\_EXT\_UI\_KEYEXTENSION**標準の Microsoft のセキュリティ設定を相互に排他的であるセキュリティ設定を提供しません。 代わりに、この種類のセキュリティ プロパティの拡張機能は IHV 定義 802.1 X を提供します。 Microsoft 802.1 X の設定と共に使用される設定。

2.  802.1 X のセキュリティ拡張機能のフレンドリ名を拡張機能を呼び出すことによってクエリ[ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)メソッド。

3.  拡張機能のクエリを実行[ **IDot11ExtUIProperty::Dot11ExtUIPropertyIsStandardSecurity** ](https://msdn.microsoft.com/library/windows/hardware/ff553760)拡張機能が、セキュリティの種類の拡張機能をサポートしているかどうかを判断するメソッド。 メソッドが設定されている場合、 *fIsStandardSecurity*パラメーターを**FALSE**、オペレーティング システムは、拡張機能のフレンドリ名を追加、**セキュリティの種類**の一覧**セキュリティ**タブ。

4.  エンドユーザーがから項目を選択すると、**セキュリティの種類**一覧で、オペレーティング システムを呼び出して、応答、 [ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetSelected** ](https://msdn.microsoft.com/library/windows/hardware/ff553753)エンド ユーザーの選択に一致するように、各拡張機能のメソッド。 値を返す最初の拡張機能**TRUE**メソッドの*pfIsSelected*パラメーターは、選択した拡張機能に決まります。 これを確認したら、オペレーティング システムには、エンド ユーザーによる選択が強調表示されます。

5.  選択したプロパティの拡張機能の呼び出し[ **IDot11ExtUIProperty::Dot11ExtUIPropertyHasConfigurationUI** ](https://msdn.microsoft.com/library/windows/hardware/ff553756)メソッドを表示できるカスタム UI プロパティ ページがあるかどうかを確認します。 メソッドの値を返す場合**TRUE**メソッドの*fHasConfigurationUI*パラメーター、オペレーティング システムが表示されます、**構成**の横にあるボタン**セキュリティの種類**一覧。

    エンドユーザーがクリックした場合、**構成**ボタン、オペレーティング システムの呼び出しが選択されているプロパティの拡張機能の[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)拡張機能のカスタム構成 UI を表示するメソッド。

6.  選択したプロパティの拡張機能の呼び出し[ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553752)メソッド。 802.11 IHV UI 拡張機能のネイティブ DLL、このメソッドを使用するその他のプロパティの拡張機能を返すことができます、**セキュリティ**ネイティブ 802.11 ネットワークの構成 UI のタブ。

    **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**メソッドに、選択したプロパティの拡張機能を追加する項目の一覧を返します、**セキュリティ**タブ。リスト内の各エントリとして書式設定、 [ **DOT11\_EXT\_UI\_プロパティ\_表示\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff548637)構造体。

    Windows vista の場合は、802.11 IHV UI 拡張機能のネイティブ DLL はのみに項目を追加、**暗号化**ボックスの一覧、**セキュリティ**タブ。一覧の各項目はその結果、 [ **DOT11\_EXT\_UI\_プロパティ\_表示\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff548637)構造体は、をいる必要があります**DOT11\_EXT\_UI\_表示\_情報\_型**の**DOT11\_EXT\_UI\_表示\_情報\_暗号**に含めるために、**暗号化**一覧。

7.  エンドユーザーが選択すると、**暗号化**一覧で、オペレーティング システムの呼び出しは選択されているプロパティの拡張機能の[ **IDot11ExtUIProperty::Dot11ExtUIPropertySetDisplayInfo**](https://msdn.microsoft.com/library/windows/hardware/ff553763)エンド ユーザーの選択に関連付けられているプロファイル データを処理するメソッド。

 

 





