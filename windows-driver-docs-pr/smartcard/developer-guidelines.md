---
title: 開発者向けのガイドライン
description: このトピックでは、使用してスマート カード ミニドライバーを開発するための一般的なガイドラインについて説明します。
ms.assetid: 48999DF6-3AC2-4DEA-8ABC-C427237B31E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cef25db934557a47597f9a103b40c8c7913636d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393103"
---
# <a name="developer-guidelines"></a>開発者向けのガイドライン


このトピックでは、開発者向けの連携、およびスマート カード ミニドライバーのスマート カードとその関連付けられているアプリケーションの想定される動作のことを知らせる開発の一般的なガイドラインについて説明します。

## <a name="span-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspangeneral-design-guidelines"></a><span id="General_Design_Guidelines"></span><span id="general_design_guidelines"></span><span id="GENERAL_DESIGN_GUIDELINES"></span>一般的なデザイン ガイドライン


カードのミニドライバーを配布する方法については論理カードのファイル システムとその他のミニドライバーの設計のガイドラインをマップする方法、**一般的なデザイン ガイドライン**セクション[スマート カード ミニドライバー概要](smart-card-minidriver-overview.md)します。

## <a name="span-idchallengeresponsemethodofunblockingsmartcardpinspanspan-idchallengeresponsemethodofunblockingsmartcardpinspanspan-idchallengeresponsemethodofunblockingsmartcardpinspanchallengeresponse-method-of-unblocking-smart-card-pin"></a><span id="Challenge_Response_Method_of_Unblocking_Smart_Card_PIN"></span><span id="challenge_response_method_of_unblocking_smart_card_pin"></span><span id="CHALLENGE_RESPONSE_METHOD_OF_UNBLOCKING_SMART_CARD_PIN"></span>スマート カード暗証番号のブロック解除のチャレンジ/レスポンス メソッド


正常にユーザーのカードのブロックを解除するこのメカニズムを使用する管理者は、管理者を特定し、発行されたチャレンジに応答データを正しく生成ができるように、カードに格納されている管理者キーを使用する必要があります。

これを行う 1 つの方法では、カードを一意に識別するために、カードの識別子を使用します。 (カードの識別子は、カードの一意の識別子です)。これは、UI では、ユーザーに何らかの形式で表現できますが、この情報をカードに適切な [apdu] コマンドを送信するプログラムを作成する可能性がありますそれ以外の場合。

この情報は、カードに秘密キーを指定し、ユーザーに発行されるチャレンジ データを適切な応答を計算するには、管理者に許可できます。

有効であり、信頼された管理者 (可能であれば限り少ない) にのみアクセス可能ないくつかのセキュリティで保護されたメカニズムを使用して、カードに格納されている管理者のシークレット キーが保持されていることと見なされます。 ただし、これは、この仕様の範囲を超えています。

詳細については、次の「チャレンジ/レスポンス メカニズム」セクションを参照してください。

## <a name="span-idenhancedpinsupportspanspan-idenhancedpinsupportspanspan-idenhancedpinsupportspanenhanced-pin-support"></a><span id="Enhanced_PIN_Support"></span><span id="enhanced_pin_support"></span><span id="ENHANCED_PIN_SUPPORT"></span>拡張 PIN のサポート


バージョン 6.0 では、複数の PIN のサポートに関して柔軟なアーキテクチャがサポートされています。 このアーキテクチャでは、各ロールが、PIN 識別子に対応するロールの新しい概念が導入されました。 カードから PIN 情報を抽出するだけでなく、暗証番号 (pin) をキー コンテナーに関連付ける、PIN 識別子が使用されます。

0 through7 に制限されて、数値の識別子で構成されます。 PIN の概念も導入しました\_設定、PIN 識別子から生成できるビットマスクであります。 PIN の使用は現在のみ下位 8 ビットを設定します。 などの条件を示すために、残りのビットを使用することも選択できます 'と'、'または'、または他の情報を今後で役に立つことがあります。 ビット マスクを適用するカードを簡単にあるように、この方法を選びました。

ユーザーを認証すること、3 の役割を持つ暗証番号 (pin) に対応すると仮定\#3。 これは、ビット マスク 0000 0100 (基本 2) に変換されます。 カードでは、現在認証されている ID とこれを記録でき、論理 AND 演算を実行してキーと Pin でのアクセス制御規則を簡単に確認できます。 設計により、同時に、カード上の複数の認証済み id を持つと、これは、v6 カードのミニドライバーをサポートするカードの要件。 ピン留めする場合、たとえば\#1 が認証され、それ以降ピン留め\#2 の認証、これらのピンのいずれかを制御する操作を許可する必要があります。

## <a name="span-idsessionpinsandsecurepinchannelspanspan-idsessionpinsandsecurepinchannelspanspan-idsessionpinsandsecurepinchannelspan-session-pins-and-secure-pin-channel"></a><span id="_Session_PINs_and_Secure_PIN_Channel"></span><span id="_session_pins_and_secure_pin_channel"></span><span id="_SESSION_PINS_AND_SECURE_PIN_CHANNEL"></span> セッション Pin とセキュリティで保護された PIN チャネル


Windows では、PIN 認証をセキュリティで保護された PIN チャネルを確立する必要があります、ミニドライバーで次の一連の操作が実行されます。 ミニドライバーとカードが従うは、次の順序で互換性がなければなりません。 具体的には、セッション Pin には、プロセス間で譲渡と過去の特定の期間だけがあります。 (任意のセッション PIN である有効なカードのコールド リセットされるまで、カードを使用することをお勧めします\_認証\_セッション\_PIN フラグ場合であっても[ **CardAuthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))。生成を使用して呼び出した\_セッション\_暗証番号 (pin) フラグを設定します)。

次の動作をサポートする必要があります。

1.  アプリケーション A を信頼済みのシステム プロセスは、スマート カードを識別するハンドルを取得し、PIN を収集します。
2.  アプリケーション A はその呼び出しカード[ **CardAuthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))ミニドライバー関数、およびパスが収集されると、カードを設定する PIN\_認証\_生成\_セッション\_ピン留めするフラグ。 これには、カードのロック解除するのには発生しません。
3.  アプリケーション A は、セッションが生成され、カードとカードのミニドライバーを識別するハンドルを解放する PIN を格納します。 カードは、コールド リセットではありません。
4.  A のアプリケーションが、セッション PIN と、リーダーであり、アプリケーション B に手順 1. で取得されたカードの名前
5.  アプリケーション B は、1 のように同じカードを取得します。
6.  アプリケーション B 呼び出し[ **CardAuthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))セッション PIN で渡すし、カードを設定\_認証\_セッション\_ピン留めするフラグ。 セッション PIN は、現在も有効ですが場合、カードは、認証済みと使用できる有効なにしてください。
7.  アプリケーション B が完了すると、カードを使用して、呼び出す[ **CardDeauthenticateEx** ](https://docs.microsoft.com/previous-versions/dn468713(v=vs.85)) deauthorize カードにします。

この動作では、次の実用的な制限があります。

-   カードは、CP の適切な値を返すことによってセッション Pin を使用するには、その機能を宣言する必要があります\_カード\_PIN\_強度\_を確認してください。
-   各検証のための暗証番号 (pin) に依存するカードは、このシステムと互換性がありません。
-   いくつかのアプリケーションを決定いつでも有効なセッション Pin をすることができます。 各ピンの PIN は 1 つのセッション、専用の場合は、次の実装はお勧めします。

    -   カードは、最新のセッションが生成された PIN を注意してくださいする必要があります。
    -   場合は、無効なセッション PIN が表示され、カード必要があります、認証に失敗し、サポートされている場合は、セッション PIN の再試行カウンターをデクリメントします。 再試行回数が 0 になるし、次の認証の試行が有効でない、セッション暗証番号 (pin) が無効になります。
    -   後続のセッション PIN のプレゼンテーションについては、新しいセッション PIN がネゴシエートされるまで失敗します。
-   セッション PIN は、システム上の異なるアプリケーションから使用することにあります。
-   セッション PIN だけは必須、暗証番号 (pin) のエンコーディングです。
-   このシステムのセキュリティは、セッション PIN の強度と生成に使用されるネゴシエーション プロトコルに限定されます。 実際のセッションの暗証番号 (pin) のネゴシエーションは、この仕様の範囲外です。 ありません要件、デザインに関するこのセクションで説明したとおりに動作する点が異なります。
-   セッション PIN は役に立つと見なされます、シークレットとして扱う必要があります。
-   カードは、無効なセッション PIN を検出できる必要があります。

## <a name="span-idread-onlycardsspanspan-idread-onlycardsspanspan-idread-onlycardsspanread-only-cards"></a><span id="Read-Only_Cards"></span><span id="read-only_cards"></span><span id="READ-ONLY_CARDS"></span>読み取り専用のカード


本質的に読み取り専用、読み取り専用のカードの新しい概念が導入されていますが、Base CSP または KSP 環境の外部に設定されているアドレス カード。 これを提供する必要があります、カードが読み取り専用の場合は、 [ **CardGetProperty** ](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85))関数 (この仕様で以前には、このセクションを参照してください)。

読み取り専用のカードは、バージョン 7 のカード ミニドライバー インターフェイスのサブセットのみをサポートする必要があり、管理者 PIN をサポートする必要はありません。

次の表には、読み取り専用のカードをサポートする必要がある関数が一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数名</th>
<th align="left">必須</th>
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468701(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAcquireContext&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468701(v=vs.85))"><strong>CardAcquireContext</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468715(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteContext&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468715(v=vs.85))"><strong>CardDeleteContext</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468704(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticatePin&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468704(v=vs.85))"><strong>CardAuthenticatePin</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468723(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetChallenge&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468723(v=vs.85))"><strong>CardGetChallenge</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468702(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticateChallenge&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468702(v=vs.85))"><strong>CardAuthenticateChallenge</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468712(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeauthenticate&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468712(v=vs.85))"><strong>CardDeauthenticate</strong></a></td>
<td align="left">[はい] (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468742(v=vs.85)" data-raw-source="[&lt;strong&gt;CardUnblockPin&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468742(v=vs.85))"><strong>CardUnblockPin</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468705(v=vs.85)" data-raw-source="[&lt;strong&gt;CardChangeAuthenticator&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468705(v=vs.85))"><strong>CardChangeAuthenticator</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468710(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateDirectory&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468710(v=vs.85))"><strong>CardCreateDirectory</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468716(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteDirectory&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468716(v=vs.85))"><strong>CardDeleteDirectory</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468736(v=vs.85)" data-raw-source="[&lt;strong&gt;CardReadFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468736(v=vs.85))"><strong>CardReadFile</strong></a></td>
<td align="left">〇</td>
<td align="left">カードのミニドライバーは、ファイル システムをエミュレートする必要があります。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))"><strong>CardCreateFile</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468727(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetFileInfo&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468727(v=vs.85))"><strong>CardGetFileInfo</strong></a></td>
<td align="left">〇</td>
<td align="left">カードのミニドライバーは、ファイル システムをエミュレートする必要があります。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468743(v=vs.85)" data-raw-source="[&lt;strong&gt;CardWriteFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468743(v=vs.85))"><strong>CardWriteFile</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468711(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteFile&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468711(v=vs.85))"><strong>CardDeleteFile</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468721(v=vs.85)" data-raw-source="[&lt;strong&gt;CardEnumFiles&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468721(v=vs.85))"><strong>CardEnumFiles</strong></a></td>
<td align="left">〇</td>
<td align="left">カードのミニドライバーは、ファイル システムをエミュレートする必要があります。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468734(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryFreeSpace&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468734(v=vs.85))"><strong>CardQueryFreeSpace</strong></a></td>
<td align="left">〇</td>
<td align="left">カードのミニドライバーは、ファイル システムをエミュレートする必要があります。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468733(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryCapabilities&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468733(v=vs.85))"><strong>CardQueryCapabilities</strong></a></td>
<td align="left">〇</td>
<td align="left">カードのミニドライバーは、ファイル システムをエミュレートする必要があります。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468708(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateContainer&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468708(v=vs.85))"><strong>CardCreateContainer</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468709(v=vs.85)" data-raw-source="[&lt;strong&gt;CardCreateContainerEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468709(v=vs.85))"><strong>CardCreateContainerEx</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468714(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeleteContainer&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468714(v=vs.85))"><strong>CardDeleteContainer</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468725(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetContainerInfo&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468725(v=vs.85))"><strong>CardGetContainerInfo</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468737(v=vs.85)" data-raw-source="[&lt;strong&gt;CardRSADecrypt&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468737(v=vs.85))"><strong>CardRSADecrypt</strong></a></td>
<td align="left">[はい] (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468707(v=vs.85)" data-raw-source="[&lt;strong&gt;CardConstructDHAgreement&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468707(v=vs.85))"><strong>CardConstructDHAgreement</strong></a></td>
<td align="left">[はい] (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468718(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeriveKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468718(v=vs.85))"><strong>CardDeriveKey</strong></a></td>
<td align="left">[はい] (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468719(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDestroyDHAgreement&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468719(v=vs.85))"><strong>CardDestroyDHAgreement</strong></a></td>
<td align="left">[はい] (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468741(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSignData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468741(v=vs.85))"><strong>CardSignData</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468735(v=vs.85)" data-raw-source="[&lt;strong&gt;CardQueryKeySizes&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468735(v=vs.85))"><strong>CardQueryKeySizes</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468703(v=vs.85)" data-raw-source="[&lt;strong&gt;CardAuthenticateEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468703(v=vs.85))"><strong>CardAuthenticateEx</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468706(v=vs.85)" data-raw-source="[&lt;strong&gt;CardChangeAuthenticatorEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468706(v=vs.85))"><strong>CardChangeAuthenticatorEx</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468713(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDeauthenticateEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468713(v=vs.85))"><strong>CardDeauthenticateEx</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468724(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetChallengeEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468724(v=vs.85))"><strong>CardGetChallengeEx</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468726(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetContainerProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468726(v=vs.85))"><strong>CardGetContainerProperty</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468738(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetContainerProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468738(v=vs.85))"><strong>CardSetContainerProperty</strong></a></td>
<td align="left">X</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468729(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85))"><strong>CardGetProperty</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468740(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468740(v=vs.85))"><strong>CardSetProperty</strong></a></td>
<td align="left">〇</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468757(v=vs.85)" data-raw-source="[&lt;strong&gt;MDImportSessionKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468757(v=vs.85))"><strong>MDImportSessionKey</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468756(v=vs.85)" data-raw-source="[&lt;strong&gt;MDEncryptData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468756(v=vs.85))"><strong>MDEncryptData</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468731(v=vs.85)" data-raw-source="[&lt;strong&gt;CardImportSessionKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468731(v=vs.85))"><strong>CardImportSessionKey</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468730(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetSharedKeyHandle&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468730(v=vs.85))"><strong>CardGetSharedKeyHandle</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468722(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetAlgorithmProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468722(v=vs.85))"><strong>CardGetAlgorithmProperty</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468728(v=vs.85)" data-raw-source="[&lt;strong&gt;CardGetKeyProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468728(v=vs.85))"><strong>CardGetKeyProperty</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468739(v=vs.85)" data-raw-source="[&lt;strong&gt;CardSetKeyProperty&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468739(v=vs.85))"><strong>CardSetKeyProperty</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468720(v=vs.85)" data-raw-source="[&lt;strong&gt;CardDestroyKey&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468720(v=vs.85))"><strong>CardDestroyKey</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/dn468732(v=vs.85)" data-raw-source="[&lt;strong&gt;CardProcessEncryptedData&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/dn468732(v=vs.85))"><strong>CardProcessEncryptedData</strong></a></td>
<td align="left">いいえ (省略可能)</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">凡例</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">〇</td>
<td align="left">この関数を実装する必要があります。</td>
</tr>
<tr class="even">
<td align="left">X</td>
<td align="left">エントリ ポイントが存在し、SCARD_E_UNSUPPORTED_FEATURE を返す必要があります。</td>
</tr>
<tr class="odd">
<td align="left">いいえ (省略可能)</td>
<td align="left">操作では、読み取り専用カードは、サポートする必要はありませんが、カードは、操作をサポートしている場合に実装することがあります。 サポートされていない場合、エントリ ポイントは SCARD_E_UNSUPPORTED_FEATURE を返す必要があります。</td>
</tr>
<tr class="even">
<td align="left">[はい] (省略可能)</td>
<td align="left">この関数は、カードは読み取り専用かどうかに関係なく、この仕様の定義に従って実装する必要があります。</td>
</tr>
</tbody>
</table>

 

読み取り専用のカードのミニドライバーを開発する際に、次の要件を検討してください。

-   すべて Base CSP または KSP ファイルが必要です、例外として ('cardcf' や 'cardid') 'msroots' ファイルが読み取り専用のカードに存在する必要があります (または、ミニドライバー インターフェイスを仮想化する必要があります)。
-   読み取り専用のカードは、プライマリのカードによって保護されているカード上の少なくとも 1 つのキーを含める必要があります (つまり、ロール\_ユーザー) ピン留めします。
-   読み取り専用のカードを許可して、管理者キーが含まれていません。 ミニドライバーはサポートされていないことが予想は、状況の場合は、 [ **CardGetChallenge**](https://docs.microsoft.com/previous-versions/dn468723(v=vs.85))、 [ **CardAuthenticateChallenge** ](https://docs.microsoft.com/previous-versions/dn468702(v=vs.85))、および[ **CardUnblockPin**](https://docs.microsoft.com/previous-versions/dn468742(v=vs.85))します。
-   読み取り専用のカード、照会されたときは、0 バイトが使用可能なと 0 の使用可能なコンテナーに返す必要があります。
-   CP のみ\_親\_ウィンドウと CP\_PIN\_コンテキスト\_読み取り専用のカードに設定する文字列プロパティを許可する必要があります。
-   読み取り専用カードは、CP\_サポート\_WIN\_X509\_登録プロパティを false にする必要があります。

## <a name="span-idcachemodesspanspan-idcachemodesspanspan-idcachemodesspancache-modes"></a><span id="Cache_Modes"></span><span id="cache_modes"></span><span id="CACHE_MODES"></span>キャッシュ モード


Base CSP または KSP がによって返されたキャッシュ モードによってキャッシュの 3 つの異なるモードをサポートしている、 [ **CardGetProperty** ](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85)) CP パラメーターで呼び出された\_カード\_キャッシュ\_モード。

-   場合、返されたフラグは CP\_キャッシュ\_モード\_GLOBAL\_キャッシュとカードの報告、CP\_読み取り\_のみ\_カード プロパティを TRUE、Base CSP または KSP データ キャッシュが、グローバル キャッシュします。 カードが読み取り専用の場合は、Base CSP または KSP は cardcf ファイルに書き込めません。 場合は、カードは、Base CSP または KSP を書き込むことが、これは今日として動作します。
-   CP の詳細については\_カード\_キャッシュ\_モードと CP\_キャッシュ\_モード\_GLOBAL\_キャッシュを参照してください[ **CardGetProperty**](https://docs.microsoft.com/previous-versions/dn468729(v=vs.85)).
-   ときに返されたフラグは、CP\_キャッシュ\_モード\_セッション\_のみ、Base CSP または KSP 動作して、カードが削除または再挿入されたことを検出した場合に、データ キャッシュをオフにします。 つまり、カードの抜き差し間の期間にセッションを定義しています。
-   キャッシュはプロセスごとにも実装されていて、グローバルではありません。 このモードは、いくつか government ステーションまたはその他の外部のサイトではなくが、ユーザーの pc では変更されない読み取り専用のカードに適しています。 (このモードは、読み取り/書き込みのカードのサポートしますが、これらのカードのグローバル キャッシュをお勧めします)。
-   アプリケーションが後で、キャッシュが st を含めることが状況を回避するには、この仕様で説明されているないキャッシュ モードを使用する必要があります、カードは読み取り専用 (Base CSP または KSP 以外の手段) によってユーザーの PC にカードを変更する可能性がある場合は、ale データ。
-   ときに、フラグは、CP\_キャッシュ\_モード\_いいえ\_キャッシュ、Base CSP または KSP 実装していない任意のデータ キャッシュします。 このモードは、カードのミニドライバー cardcf ファイルの書き込みをサポートしていないが、カードの状態を変更できますが適しています。 カードのミニドライバーは、任意のレイヤーでキャッシュを実行するかどうかを決定します。

## <a name="span-idchallengeresponsemechanismspanspan-idchallengeresponsemechanismspanspan-idchallengeresponsemechanismspan-challengeresponse-mechanism"></a><span id="_Challenge_Response_Mechanism"></span><span id="_challenge_response_mechanism"></span><span id="_CHALLENGE_RESPONSE_MECHANISM"></span> チャレンジ/レスポンス メカニズム


カードのミニドライバー インターフェイスには、チャレンジ/レスポンス認証メカニズムがサポートしています。 カードには、1 つ以上の 8 バイトのブロックのチャレンジを生成する必要があります。 認証エンティティが 168 ビット キーを使用して、CBC モードで動作を操作する Triple DES (3 des) を使用してチャレンジを暗号化して、応答を計算します (およびパリティ ビットを無視します)。

カードは、次のメソッドのいずれかを使用して、応答を確認します。

-   以前に発行されたチャレンジに暗号化操作を繰り返すと、結果を比較します。
-   応答を復号化し、チャレンジに結果を比較します。

結果の値が同じ場合は、認証が成功します。

カードと認証のエンティティの両方に同じ対称キーを使用する必要があります。

次のサンプル コードでは、認証エンティティが応答を計算する方法について説明します。 このコードは、関連付けられているすべての保証については説明しませんし、例とガイダンスとしてだけで提供されます。

```ManagedCPlusPlus
#include <windows.h>
#include <wincrypt.h>
#include <winscard.h>
#include <stdlib.h>
#include <stdio.h>
#include <memory.h>


int __cdecl wmain(int argc, __in_ecount(argc) WCHAR **wargv)
{
    //Acquire the context Use CryptAcquireContext

    HCRYPTPROV hProv= 0;
    DWORD dwMode=CRYPT_MODE_ECB;
    BYTE *pbLocData = NULL,tempbyte;
    DWORD cbLocData = 8, count = 0;
    HCRYPTKEY hKey = 0;
    BYTE rgEncByte [] = {0xA8,0x92,0xD7,0x56,0x01,0x61,0x7C,0x5D };

    BYTE DesKeyBlob [] = {
        0x08, 0x02, 0x00, 0x00, 0x03, 0x66, 0x00, 0x00,
        0x18, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00
    };

    pbLocData = (BYTE *) malloc (sizeof(BYTE)*cbLocData);
    memcpy(pbLocData,rgEncByte,cbLocData);

    if (!CryptAcquireContext(
            &hProv,
            NULL,
            L"Microsoft Enhanced Cryptographic Provider V1.0",
            PROV_RSA_FULL,
            CRYPT_VERIFYCONTEXT))
    {
        printf("Acquire context failed with 0x%08x \n", GetLastError());
        goto Cleanup;
    }
    if (!CryptImportKey(
            hProv,
            DesKeyBlob,
            sizeof(DesKeyBlob),
            0,
            0,
            &hKey ) )
    {
        printf("Error 0x%08x in importing the 3Des key \n", GetLastError());
        goto Cleanup;
    }
    if (!CryptSetKeyParam(
            hKey,
            KP_MODE,
            (BYTE *)&dwMode,
            0))
    {
        printf("Error 0x%08x in CryptSetKeyParam \n", GetLastError());
        goto Cleanup;
    }
    if (!CryptEncrypt(
            hKey,
            0,
            FALSE,
            0,
            pbLocData,
            &cbLocData,
            cbLocData))
    {
        printf("Error 0x%08x in CryptEncrypt call \n", GetLastError());
        goto Cleanup;
    }

    for (count=0; count < cbLocData; ++count)
    {
        printf("0x%02x",pbLocData[count]);
    }
    printf("\n");

Cleanup:    
    if (hKey)
    {
        CryptDestroyKey(hKey);
        hKey = 0;
    }
    if (pbLocData)
    {
        free(pbLocData);
        pbLocData = NULL;
    }
    if (hProv)
    {
        CryptReleaseContext(hProv,0);
    }

    return 0;
}
```

## <a name="span-idinteroperabilitywithmsrootsspanspan-idinteroperabilitywithmsrootsspanspan-idinteroperabilitywithmsrootsspan-interoperability-with-msroots"></a><span id="_Interoperability_with_msroots"></span><span id="_interoperability_with_msroots"></span><span id="_INTEROPERABILITY_WITH_MSROOTS"></span> Msroots との相互運用


Msroots ファイルは、PKCS\#エンタープライズ向けの 7 の書式設定された証明書ストアの信頼されたルート。 (ファイルは空のコンテンツと空のシグネチャで証明書のバッグとは、によって書き込みし、読み取り Base CSP。)カードのミニドライバーの開発者は、このファイルを処理するためにカードのミニドライバーで特別なコードを記述する必要はありません。 Msroots で証明書を格納するファイル、コードなどのプロパティ\_msroots ファイルがコンピューター ストアから別の形式で証明書を格納するため、署名の EKU はスマート カードに反映されません。 読み取りまたは他のアプリケーションからこのファイルを記述する開発者は、データにアクセスするのに次のサンプル コード スニペットを使用できます。

### <a name="span-idreadoperationsspanspan-idreadoperationsspanspan-idreadoperationsspanread-operations"></a><span id="Read_operations"></span><span id="read_operations"></span><span id="READ_OPERATIONS"></span>読み取り操作

```ManagedCPlusPlus
if (FALSE == CryptQueryObject(CERT_QUERY_OBJECT_BLOB,
                                &dbStore,
                                CERT_QUERY_CONTENT_FLAG_PKCS7_SIGNED,
                                CERT_QUERY_FORMAT_FLAG_BINARY,
                                0,
                                NULL,
                                NULL,
                                NULL,
                                phCertStore,
                                NULL,
                                NULL))
{
    dwSts = GetLastError();
}
```

### <a name="span-idwriteoperationsspanspan-idwriteoperationsspanspan-idwriteoperationsspanwrite-operations"></a><span id="Write_operations"></span><span id="write_operations"></span><span id="WRITE_OPERATIONS"></span>書き込み操作

```ManagedCPlusPlus
// Serialize the store

if (FALSE == CertSaveStore( hCertStore,
                            PKCS_7_ASN_ENCODING | X509_ASN_ENCODING,
                            CERT_STORE_SAVE_AS_PKCS7,
                            CERT_STORE_SAVE_TO_MEMORY,
                            &dbStore,
                            0))
{
    dwSts = GetLastError();
    goto Ret;
}

dbStore.pbData = CspAllocH(dbStore.cbData);

if (NULL == dbStore.pbData)
{
    dwSts = ERROR_NOT_ENOUGH_MEMORY;
    goto Ret;
}

if (FALSE == CertSaveStore( hCertStore,
                            PKCS_7_ASN_ENCODING | X509_ASN_ENCODING,
                            CERT_STORE_SAVE_AS_PKCS7,
                            CERT_STORE_SAVE_TO_MEMORY,
                            &dbStore,
                            0))
{
    dwSts = GetLastError();
    goto Ret;
}
```

## <a name="span-idgrouppolicysettingsformicrosoftbasesmartcardcspspanspan-idgrouppolicysettingsformicrosoftbasesmartcardcspspanspan-idgrouppolicysettingsformicrosoftbasesmartcardcspspangroup-policy-settings-for-microsoft-base-smart-card-csp"></a><span id="Group_Policy_Settings_for_Microsoft_Base_Smart_Card_CSP"></span><span id="group_policy_settings_for_microsoft_base_smart_card_csp"></span><span id="GROUP_POLICY_SETTINGS_FOR_MICROSOFT_BASE_SMART_CARD_CSP"></span>Microsoft スマート カード CSP のグループ ポリシー設定


Microsoft Base Smart Card Crypto Service Provider のグループ ポリシー設定にある\[HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\暗号化\\既定\\プロバイダー\\Microsoft Base Smart Card の Crypto Provider\]します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Key</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">DefaultPrivateKeyLenBits</td>
<td align="left"><p>dword:00000400</p>
<p>既定のキーの生成パラメーター: 1024 ビットのキー。</p></td>
</tr>
<tr class="even">
<td align="left">RequireOnCardPrivateKeyGen</td>
<td align="left"><p>dword:00000000</p>
<p>これには、カードに秘密のキーの生成 (既定値) を要求するためのフラグを設定します。 この値が設定されている場合は、カードにホスト上で生成されるキーをインポートすることができます。 これは、カードのカードのキーの生成をサポートしていないか、キー エスクローが必要な場合に使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left">TransactionTimeoutMilliseconds</td>
<td align="left"><p>dword:000005dc</p>
<p>1500、1.5 秒は、カードにトランザクションを保持するための既定のタイムアウトです。</p></td>
</tr>
<tr class="even">
<td align="left">AllowPrivateSignatureKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>キーのアーカイブの用途は、署名キーをインポートできるようにします。</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateExchangeKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>キーのアーカイブの用途は、交換キーをインポートできるようにします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idgrouppolicysettingsformicrosoftcngsmartcardkspspanspan-idgrouppolicysettingsformicrosoftcngsmartcardkspspanspan-idgrouppolicysettingsformicrosoftcngsmartcardkspspan-group-policy-settings-for-microsoft-cng-smart-card-ksp"></a><span id="_Group_Policy_Settings_for_Microsoft_CNG_Smart_Card_KSP"></span><span id="_group_policy_settings_for_microsoft_cng_smart_card_ksp"></span><span id="_GROUP_POLICY_SETTINGS_FOR_MICROSOFT_CNG_SMART_CARD_KSP"></span> Microsoft CNG スマート カード KSP のグループ ポリシー設定


Microsoft CNG スマート カード キー記憶域プロバイダーのグループ ポリシー設定にある\[HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\暗号化\\プロバイダー\\Microsoft スマート カード キー記憶域プロバイダー\]します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Key</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">DefaultPrivateKeyLenBits</td>
<td align="left"><p>dword:00000400</p>
<p>既定のキーの生成パラメーター: 1024 ビットのキー。</p></td>
</tr>
<tr class="even">
<td align="left">RequireOnCardPrivateKeyGen</td>
<td align="left"><p>dword:00000000</p>
<p>これには、カードに秘密のキーの生成 (既定値) を要求するためのフラグを設定します。 この値が設定されている場合は、カードにホスト上で生成されるキーをインポートすることができます。 これは、カードのカードのキーの生成をサポートしていないか、キー エスクローが必要な場合に使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left">TransactionTimeoutMilliseconds</td>
<td align="left"><p>dword:000005dc</p>
<p>1500、1.5 秒は、カードにトランザクションを保持するための既定のタイムアウトです。</p></td>
</tr>
<tr class="even">
<td align="left">AllowPrivateSignatureKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>キーのアーカイブの用途は、署名キーをインポートできるようにします。</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateExchangeKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>キーのアーカイブの用途は、交換キーをインポートできるようにします。</p></td>
</tr>
<tr class="even">
<td align="left">AllocPrivateECDHEKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>ECDH キー、キーのアーカイブの用途は、インポートできるようにします</p></td>
</tr>
<tr class="odd">
<td align="left">AllowPrivateECDSAKeyImport</td>
<td align="left"><p>dword:00000000</p>
<p>ECDSA キー、キーのアーカイブの用途は、インポートできるようにします</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idspecialconsiderationsspanspan-idspecialconsiderationsspanspan-idspecialconsiderationsspanspecial-considerations"></a><span id="Special_Considerations"></span><span id="special_considerations"></span><span id="SPECIAL_CONSIDERATIONS"></span>特別な考慮事項


-   Windows Vista Service Pack 1 (SP1) では、オペレーティング システムがセーフ モードで実行中にスマート カードの暗証番号 (pin) が必要な操作はありません可能であれば、Windows ログオン以外。
-   次のいずれかの通話 CryptAcquireContext フラグのユーザー暗証番号 (pin) 認証のプロンプト\_コンテナーに割り当てられている実際の PIN に関係なく PIN:

    -   CRYPT\_NEWKEYSET
    -   CRYPT\_既定\_コンテナー\_(省略可能)
    -   CRYPT\_DELETEKEYSET
    -   CRYPT\_VERIFYCONTEXT
-   [**CardDeleteContext** ](https://docs.microsoft.com/previous-versions/dn468715(v=vs.85))後も呼び出すことができる*DllMain* DLL で呼び出されました\_プロセス\_デタッチします。

 

 

