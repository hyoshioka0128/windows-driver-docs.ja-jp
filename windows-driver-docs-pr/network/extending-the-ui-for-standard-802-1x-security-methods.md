---
title: 標準 802.1X セキュリティ メソッドの UI の拡張
description: 標準 802.1X セキュリティ メソッドの UI の拡張
ms.assetid: e80e82e9-3ad3-48d0-a569-169de356ebba
keywords:
- 802.1 X の標準的なセキュリティ WDK IHV UI 拡張機能の DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7516263b1381464a8724ccd99acc024acf904acd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570163"
---
# <a name="extending-the-ui-for-standard-8021x-security-methods"></a>標準 802.1X セキュリティ メソッドの UI の拡張




 

802.11 IHV UI 拡張機能のネイティブ DLL が、ネットワーク構成ユーザー インターフェイスの拡張できます 802.11 IHV 拡張機能のネイティブ DLL では、オペレーティング システムの 802.1 X のセキュリティ メソッドで使用できる独自の暗号化の拡張機能をサポートする場合 (UI') s **セキュリティ** タブ、これらのユーザーの構成を許可する拡張機能。 802.11 802.1 X のネイティブ モジュールを拡張する方法の詳細については、[インターフェイス ネイティブ 802.11 802.1 X モジュール](interface-to-the-native-802-11-802-1x-module.md)を参照してください。

ネットワークの構成 UI やその他のネイティブの 802.11 コンポーネントに関する詳細については、[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)を参照してください。

表示にする前に、**セキュリティ** タブで、オペレーティング システムは次の処理します。

1.  呼び出すことによって、セキュリティ プロパティの拡張機能に対してネイティブ 802.11 IHV UI 拡張 DLL のクエリ、 [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)メソッド。 オペレーティング システムの値を渡す**DOT11\_EXT\_UI\_KEYEXTENSION**メソッドの*ExtType*パラメーター。

    型のプロパティの拡張機能**DOT11\_EXT\_UI\_KEYEXTENSION**標準の Microsoft のセキュリティ設定を相互に排他的であるセキュリティ設定を提供しません。 代わりに、この種類のセキュリティ プロパティの拡張機能は IHV 定義 802.1 X を提供します。 Microsoft 802.1 X の設定と共に使用される設定。

2.  802.1 X のセキュリティ拡張機能のフレンドリ名を拡張機能を呼び出すことによってクエリ[ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)メソッド。

3.  拡張機能のクエリを実行[ **IDot11ExtUIProperty::Dot11ExtUIPropertyIsStandardSecurity** ](https://msdn.microsoft.com/library/windows/hardware/ff553760)拡張機能が、セキュリティの種類の拡張機能をサポートしているかどうかを判断するメソッド。 メソッドが設定されている場合、 *fIsStandardSecurity*パラメーターを**TRUE**、オペレーティング システムは、拡張機能のフレンドリ名を追加できません、**セキュリティの種類**の一覧**セキュリティ**タブ。

    このような状況では、拡張機能は、オペレーティング システムでサポートされているセキュリティ設定に機能を追加します。 このメソッドで拡張セキュリティ設定の種類を指定します、 *dot11ExtUISecurityType*パラメーター。

4.  エンドユーザーがから項目を選択すると、**セキュリティの種類**一覧で、オペレーティング システムを呼び出して、応答、 [ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetSelected** ](https://msdn.microsoft.com/library/windows/hardware/ff553753)エンド ユーザーの選択に一致するように、各拡張機能のメソッド。 値を返す最初の拡張機能**TRUE**メソッドの*pfIsSelected*パラメーターは、選択した拡張機能に決まります。 これを確認したら、オペレーティング システムには、エンド ユーザーによる選択が強調表示されます。

5.  エンドユーザーがから標準的なセキュリティ設定の項目を選択すると、**セキュリティの種類**一覧で、オペレーティング システムの呼び出し、 [ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**](https://msdn.microsoft.com/library/windows/hardware/ff553752)セキュリティ メソッドを拡張するプロパティの拡張機能のメソッド。 を通じて、 **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**メソッドに追加するには、その他の項目が 802.11 IHV UI 拡張機能のネイティブ DLL に返すことができます、**セキュリティ**ネイティブ 802.11 のタブネットワークの構成 UI です。

    **IDot11ExtUIProperty::Dot11ExtUIPropertyGetDisplayInfo**メソッド、プロパティの拡張機能でサポートされている拡張表示プロパティの一覧を返します。 リスト内の各項目として書式設定、 [ **DOT11\_EXT\_UI\_プロパティ\_表示\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff548637)構造体。

    Windows vista の場合は、802.11 IHV UI 拡張機能のネイティブ DLL はのみに項目を追加、**暗号化**ボックスの一覧、**セキュリティ**タブ。その結果、各エントリの一覧内で[ **DOT11\_EXT\_UI\_プロパティ\_表示\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff548637)構造体は、をいる必要があります**DOT11\_EXT\_UI\_表示\_情報\_型**の**DOT11\_EXT\_UI\_表示\_情報\_暗号**に含めるために、**暗号化**一覧。

6.  エンドユーザーが選択すると、**暗号化**一覧で、オペレーティング システムのプロパティの拡張機能が呼び出す[ **IDot11ExtUIProperty::Dot11ExtUIPropertySetDisplayInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553763)、エンド ユーザーの選択に関連付けられているプロファイル データを処理するメソッド。

 

 





