---
title: ワイヤレス セキュリティ プロパティの拡張
description: ワイヤレス セキュリティ プロパティの拡張
ms.assetid: be6af188-fa60-4ac8-a699-97a3baaec6be
keywords:
- IHV UI 拡張 DLL WDK ネイティブ 802.11、セキュリティのプロパティ
- WDK ネイティブ 802.11 IHV UI 拡張 DLL のセキュリティのプロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49c9ad86cb3185d24e3d1df13bb29c9c9bd079d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347415"
---
# <a name="extending-wireless-security-properties"></a>ワイヤレス セキュリティ プロパティの拡張




 

このトピックでは、ネイティブの 802.11 IHV UI の拡張 DLL でのプロパティを拡張する方法について説明します、**セキュリティ**ネットワーク構成ユーザー インターフェイス (UI) を通じて表示されるタブ。 802.11 IHV UI 拡張機能のネイティブ DLL では、このような状況では、プロパティの追加、**セキュリティ**802.11 802.1 X のネイティブ モジュールから相互に排他的である独自のセキュリティ設定 タブ。

802.11 IHV UI 拡張機能のネイティブ DLL は、802.11 802.1 X のネイティブ モジュールでサポートされているセキュリティと暗号化のメソッドを拡張することもできます。 方法は、DLL の詳細については、次を参照してください。[を拡張する Microsoft 802.1 X のセキュリティ設定](extending-microsoft-802-1x-security-settings.md)します。

ネットワークの構成 UI やその他のネイティブの 802.11 コンポーネントに関する詳細については、次を参照してください。[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)します。

表示にする前に、**セキュリティ** タブで、オペレーティング システムは次の処理します。

1.  呼び出すことによって、セキュリティ プロパティの拡張機能に対してネイティブ 802.11 IHV UI 拡張 DLL のクエリ、 [ **IDot11ExtUI::GetDot11ExtUIProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff553776)メソッド。 オペレーティング システムの値を渡す**DOT11\_EXT\_UI\_セキュリティ**メソッドの*ExtType*パラメーター。

    802.11 IHV UI 拡張機能のネイティブ DLL には、型の 1 つまたは複数のプロパティがサポートされている場合**DOT11\_EXT\_UI\_セキュリティ**、DLL を返します (メソッドのを通じて*ppDot11ExtUIProperty*パラメーター) の一覧[IDot11ExtUIProperty COM インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553746)DLL でサポートされているセキュリティのプロパティの拡張機能。 セキュリティのプロパティを拡張するために使用する COM インターフェイスの詳細については、次を参照してください。[ネイティブ 802.11 IHV UI 拡張機能の COM インターフェイス](native-802-11-ihv-ui-extensions-com-interfaces.md)します。

2.  セキュリティ拡張機能のフレンドリ名を拡張機能を呼び出すことによってクエリ[ **IDot11ExtUIProperty::GetDot11ExtUIPropertyFriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff553768)メソッド。 オペレーティング システムの下部にある独自のセキュリティ設定の一覧に表示名を追加する、**セキュリティ**タブ。

3.  オペレーティング システムを呼び出すが、エンドユーザーは、この一覧から項目を選択した場合、 [ **IDot11ExtUIProperty::Dot11ExtUIPropertyGetSelected** ](https://msdn.microsoft.com/library/windows/hardware/ff553753)メソッドの各セキュリティ拡張機能の[IDot11ExtUIProperty COM インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553746)します。 値を返す最初の拡張機能**TRUE**メソッドの*pfIsSelected*パラメーターは、選択した拡張機能に決まります。 一覧で選択したエントリを強調表示し、されます。

4.  クエリを選択した設定の[ **IDot11ExtUIProperty::Dot11ExtUIPropertyHasConfigurationUI** ](https://msdn.microsoft.com/library/windows/hardware/ff553756)メソッドを表示できるカスタム UI プロパティ ページがあるかどうかを確認します。 メソッドによって返される場合、 *fHasConfigurationUI*パラメーターに設定**TRUE**、オペレーティング システムは追加、**構成**独自仕様のセキュリティの一覧の横にあるボタンをクリックします。設定。

選択した独自のセキュリティ設定が構成 UI と、エンドユーザーをサポートしている場合をクリックする、**構成**ボタン、オペレーティング システムの呼び出しの設定の[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)カスタム UI を起動するメソッド。 オペレーティング システムは、メソッドの設定の現在のプロファイル データを渡します*bstrIHVProfile*引数。

プロファイル データは境界付けられた XML フラグメントとして書式設定、 &lt;IHV&gt; &lt;/IHV&gt; XML タグ。 これらのタグ内の XML データは、IHV の実装に固有し、オペレーティング システムに対して非透過的です。 ネイティブの 802.11 プロファイル データの書式設定に関する詳細については、Microsoft Windows SDK 内のドキュメントを参照してください。

カスタム ui 設定のプロファイル データが変更されたかどうか[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)メソッドが戻る前に、次を行う必要があります。

-   変更されたプロファイル データの文字列バッファーを割り当てるし、メソッドの使用、バッファーへのポインターを返す*bstrModifiedIHVProfile*パラメーター。
    **注**  設定の[ **IDot11ExtUIProperty::DisplayDot11ExtUIProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff553749)メソッドによって参照されるデータは変更しないで、 *bstrIHVProfile*引数。

     

-   設定、 *pbIsModified*引数**TRUE**します。

 

 





