---
title: ワイヤレス接続のプロパティを拡張します。
description: ワイヤレス接続のプロパティを拡張します。
ms.assetid: 77efa8f8-0b94-46b7-89d1-ec9c2c180845
keywords:
- IHV UI 拡張 DLL WDK ネイティブ 802.11 ワイヤレス接続のプロパティ
- ワイヤレス接続のプロパティ WDK ネイティブ 802.11 IHV UI 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b04c505fc8c572b2e24134ef4a33c8ec6525ab0e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538142"
---
# <a name="extending-wireless-connection-properties"></a>ワイヤレス接続のプロパティを拡張します。




 

このトピックでは、ネイティブの 802.11 IHV UI の拡張 DLL がでプロパティを拡張する方法について説明します、**接続**ネットワーク構成ユーザー インターフェイス (UI) を通じて表示されるタブ。 802.11 IHV UI 拡張機能のネイティブ DLL では、このような状況では、プロパティの追加、**接続**の独自の接続設定 タブ。

ネットワークの構成 UI やその他のネイティブの 802.11 コンポーネントに関する詳細については、[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)を参照してください。

表示にする前に、**接続** タブで、オペレーティング システムは次の処理します。

1.  クエリをネイティブ 802.11 IHV UI 拡張機能の DLL をその接続のプロパティを呼び出すことによって、 [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)メソッド。 オペレーティング システムの値を渡す**DOT11\_EXT\_UI\_接続**メソッドの*ExtType*パラメーター。

    802.11 IHV UI 拡張機能のネイティブ DLL が型のプロパティをサポートしているか**DOT11\_EXT\_UI\_接続**、DLL を返します (メソッドのを通じて*ppDot11ExtUIProperty*パラメーター) のアドレス、 [IDot11ExtUIProperty COM インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553746)、接続プロパティの拡張機能を実装します。 接続のプロパティの拡張に使用される COM インターフェイスの詳細については、[ネイティブ 802.11 IHV UI 拡張機能の COM インターフェイス](native-802-11-ihv-ui-extensions-com-interfaces.md)を参照してください。

    **注**  For Windows Vista 802.11 IHV UI 拡張機能のネイティブ DLL 返す必要がありますいない 1 つ以上[IDot11ExtUI COM インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553769)接続プロパティの拡張機能。

     

2.  オペレーティング システムが、拡張機能を呼び出すことによって、プロパティの拡張機能のフレンドリ名をクエリする 802.11 IHV UI 拡張機能のネイティブ DLL では、接続プロパティをサポートする場合[ **IDot11ExtUIProperty:。GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)メソッド。 オペレーティング システムがテキスト内でフレンドリ名を挿入します"を有効にする*xxx*接続の設定"、"*xxx*"プロパティの拡張機能の表示名です。 オペレーティング システムのチェック ボックスと共にこのテキストが表示されます、**接続**タブ。

3.  表示できるカスタムの UI プロパティがあるかどうかを確認する拡張機能を照会します。 オペレーティング システムは、拡張機能を呼び出すことによって[ **IDot11ExtUIProperty::Dot11ExtUIPropertyHasConfigurationUI** ](https://msdn.microsoft.com/library/windows/hardware/ff553756)メソッド。 かどうか、接続プロパティの拡張機能は、カスタム UI プロパティをサポートするオペレーティング システムを追加、**構成**プロパティのチェック ボックスの下のボタンをクリックします。

選択した独自の接続設定が構成 UI と、エンドユーザーをサポートしている場合をクリックする、**構成**ボタン、**接続** タブで、オペレーティング システムを呼び出す接続のプロパティ拡張機能の[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)カスタム UI を起動するメソッド。 オペレーティング システムは、メソッドの使用、拡張機能の現在のプロファイル データを渡します*bstrIHVProfile*引数。

プロファイル データは境界付けられた XML フラグメントとして書式設定、 &lt;IHV&gt; &lt;/IHV&gt; XML タグ。 これらのタグ内の XML データは、IHV の実装に固有し、オペレーティング システムに対して非透過的です。 ネイティブの 802.11 プロファイル データの書式設定に関する詳細については、Microsoft Windows SDK 内のドキュメントを参照してください。

カスタム UI を使用、拡張機能のプロファイル データが変更されたかどうか[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)メソッドが戻る前に、次を行う必要があります。

-   変更されたプロファイル データの文字列バッファーを割り当てるし、メソッドの使用、バッファーへのポインターを返す*bstrModifiedIHVProfile*パラメーター。
    **注**  拡張機能の[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)メソッドで参照されるデータは変更しないで、 *bstrIHVProfile*引数。

     

-   設定、 *pbIsModified*引数**TRUE**します。

 

 





