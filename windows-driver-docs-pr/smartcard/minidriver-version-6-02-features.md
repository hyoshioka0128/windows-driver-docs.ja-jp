---
title: ミニドライバー バージョン 6.02 機能
description: ミニドライバー バージョン 6.02 機能
ms.assetid: 8BF4B63B-B723-4899-BCAF-7826FAFF2155
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4c7c80de36691644eae17970dcf7481d8489dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550203"
---
# <a name="minidriver-version-602-features"></a>ミニドライバー バージョン 6.02 機能


このバージョンでは、次の機能が導入されました。

## <a name="span-idenhancedsupportforpinsspanspan-idenhancedsupportforpinsspanspan-idenhancedsupportforpinsspanenhanced-support-for-pins"></a><span id="Enhanced_Support_for_PINs"></span><span id="enhanced_support_for_pins"></span><span id="ENHANCED_SUPPORT_FOR_PINS"></span>Pin のサポートの強化


スマート カード ミニドライバーの仕様のバージョン 6 では、Pin のサポートを強化します。 このバージョンには、論理 PIN オブジェクトの新しい概念が導入されています。 開発者は、暗証番号 (pin) のオブジェクト アーキテクチャを使用することで、入力を求める Windows の暗証番号 (pin) を制御し、柔軟で幅広い一連のシナリオを有効にします。 暗証番号 (pin) オブジェクトは、可能性がありますまたはカードの実際の物理ピンに対応していないと、カードのミニドライバー Windows での PIN に関連する動作を制御するための手段として表示する必要があります。

新しい Api セット、を通じてカード ミニドライバーの開発者できるようになりました。

-   (最大 8 個のピンの合計) の 2 つ以上の Pin を使用するカードをサポートします。
-   セッション PIN を Windows に実際の PIN の代わりにキャッシュに戻ります。
-   どのような文字列を中の表示、ユーザー PIN プロンプトを制御します。
-   特定のキーが要求されたときに PIN を要求する Windows を示します。
-   カードまたは PIN プロンプト (空のピン留め) なしのコンテナーへのアクセスを許可します。

詳細については、「拡張 PIN のサポート」セクションを参照してください。[開発者ガイドライン](developer-guidelines.md)します。

リファレンス情報は、[カードのピン留め操作](card-pin-operations.md)を参照してください。

このバージョンで追加された新しい Api は次のとおりです。

-   [**CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)
-   [**CardGetChallengeEx**](https://msdn.microsoft.com/library/windows/hardware/dn468724)
-   [**CardDeauthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468713)
-   [**CardChangeAuthenticatorEx**](https://msdn.microsoft.com/library/windows/hardware/dn468706)

**重要な**  すべてプロビジョニング システムが複数の Pin をサポート。 そのため、注意が必要 フィールドに、カードのプロビジョニング システムで更新できるキーのピンを適用するときにします。

 

## <a name="span-idsupportforread-onlycardsspanspan-idsupportforread-onlycardsspanspan-idsupportforread-onlycardsspansupport-for-read-only-cards"></a><span id="Support_for_Read-Only_Cards"></span><span id="support_for_read-only_cards"></span><span id="SUPPORT_FOR_READ-ONLY_CARDS"></span>読み取り専用のカードのサポート


セキュリティで保護された PIN チャネルは、Windows と PIN 認証用のスマート カードの間のセキュリティで保護されたチャネルの確立後にセキュリティで保護された PIN プロンプトを使用した Service Pack 1 (SP1) Windows Vista の機能です。 セキュリティで保護された PIN チャネルは、オペレーティング システムのコンポーネントとカードに送信中を旅行中に傍受を防ぐため、カードの暗証番号 (pin) を保護します。

次の視覚的効果の Windows ログオンと同じ PIN の入力を求め、ユーザーがいることを意味要求する前に ALT + CTL + DEL キーを押して PIN プロンプトをセキュリティで保護します。 暗証番号 (pin) をセキュリティで保護されたプロンプトが暗証番号 (pin) の収集のなりすましの原因の PIN プロンプト ダイアログ ボックスでのリスクを軽減します。

セキュリティで保護された PIN チャネルを制御し、一般的な条件のグループ ポリシー設定によって、暗証番号 (pin) のオブジェクトの特定の属性によってもトリガーします。

セキュリティで保護された PIN チャネルの詳細については、"セッション Pin"のセクションを参照してください。[開発者ガイドライン](developer-guidelines.md)します。

この機能に関連する新しい API が含まれる[ **CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)します。

## <a name="span-idexternalpinsupportspanspan-idexternalpinsupportspanspan-idexternalpinsupportspan-external-pin-support"></a><span id="_External_PIN_Support"></span><span id="_external_pin_support"></span><span id="_EXTERNAL_PIN_SUPPORT"></span> 外部 PIN のサポート


外部の PIN のサポートは、PC のユーザーから収集された PIN です。 外部の暗証番号 (pin) シナリオの例は次のとおりです。

-   PIN は暗証番号入力パッド リーダーで収集されます。
-   スマート カードは、それにアタッチされている指紋リーダーを備え、指紋テンプレートを使用したカードの PIN の代わりとして、一致を実行します。

外部 PIN モードでスマート カードへ PIN 認証が必要な場合は、Windows は、PIN をユーザーを要求していないがではなく、ユーザーに通知されることがなくすぐにミニドライバーの認証 API を呼び出します。 オペレーティング システムを介さずに、実際の認証と PIN の収集が発生することが期待されます。

必要に応じて、および特定の制限、ミニドライバーは、独自のユーザー インターフェイス (UI) をユーザーが PIN の収集の関係における特定のアクションを実行するように指示を表示する許可します。 はなく、外部から収集する際に PIN を待機している Windows ユーザーに指示するが、実際には、ユーザーから PIN を収集するために、このような UI を使用することには必要ありません。 ミニドライバーは、コンテキストがサイレント モードと UI 要素を作成する特定のウィンドウ ハンドルを使用すると予測はときに、UI を表示する許可されていません。 詳細についてを参照[ **CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)、および[ **CardSetProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468740)します。

一時的なセッション PIN を返すことができるカードは、後続のキャッシングを Windows にこのような PIN を返す可能性があります。 このような場合では、Windows は、カードには、セッション PIN が無効にするまでにカードの認証以降のすべてのセッション PIN を紹介します。 詳細については、[ **CardAuthenticateEx**](https://msdn.microsoft.com/library/windows/hardware/dn468703)を参照してください。

 

 





