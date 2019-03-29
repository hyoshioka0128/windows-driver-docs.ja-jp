---
title: ミニドライバー バージョン 7.06 の機能
description: ミニドライバー バージョン 7.06 の機能
ms.assetid: 6066C6F9-DF03-4886-A5AE-FFE50B2B34D8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2a6d6271c0492555495aeb94cee9832991ce5d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571562"
---
# <a name="minidriver-version-706-features"></a>ミニドライバー バージョン 7.06 の機能


このバージョンでは、次の機能が導入されました。

## <a name="span-idsecurekeyinjectionspanspan-idsecurekeyinjectionspanspan-idsecurekeyinjectionspansecure-key-injection"></a><span id="Secure_Key_Injection"></span><span id="secure_key_injection"></span><span id="SECURE_KEY_INJECTION"></span>セキュリティで保護されたキーの挿入


この機能は、スマート カードから切断されているコンピューターで実行している、アプリケーションは他のコンピューターに接続されているスマート カードに機密データをインポートする必要がある場合に便利です。

セキュリティで保護されたキーの挿入の 1 つの一般的なシナリオでは、サーバー上で実行している証明機関 (CA) は、次の操作を実行する必要がありますとを示します。

-   サーバー上のキーのペアを生成します。
-   ユーザー キーをアーカイブします。
-   ユーザーのコンピューターに挿入されたスマート カードには、キーのペアをインポートします。

開発者には、次のセキュリティで保護されたキー挿入用に導入された新しい Api、データ構造を使用できます。

-   プロパティが、カードがセキュリティで保護されたキーの挿入をサポートしているかどうかを判断するためにスマート カード フレームワークをサポートします。
-   Pin、管理者キーと非対称キーの組などのデータの暗号化のための対称キーを確立します。 セッション キーは、スマート カードにインポートできます。
-   暗号化しにインポートして、スマート カード上で処理できる形式にデータをカプセル化します。
-   スマート カードにセッション キーで暗号化されたデータを復号化します。

暗号化されたデータを渡すために、次の構造は、このバージョンの仕様で定義されます。

-   [**カード\_認証**](https://msdn.microsoft.com/library/windows/hardware/dn468744)
-   [**カード\_認証\_応答**](https://msdn.microsoft.com/library/windows/hardware/dn468745)
-   [**カード\_変更\_AUTHENTICATOR**](https://msdn.microsoft.com/library/windows/hardware/dn468746)
-   [**カード\_変更\_AUTHENTICATOR\_応答**](https://msdn.microsoft.com/library/windows/hardware/dn468747)
-   [**カード\_ENCRYPTED\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468749)
-   [**カード\_インポート\_キー ペア**](https://msdn.microsoft.com/library/windows/hardware/dn468750)

セキュリティで保護されたキーの挿入の次のカード プロパティは、この仕様のバージョン 7 で定義されます。 これらのプロパティの詳細については、次を参照してください。 [ **CardGetProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468729)します。

-   CP\_キー\_インポート\_サポート
-   CP\_ENUM\_アルゴリズム
-   CP\_PADDING\_スキーム
-   CP\_チェーン\_モード

この仕様のバージョン 7 でセキュリティで保護されたキー挿入の次の Api が追加されました。 詳細については、次を参照してください。[セキュリティで保護されたキーの挿入](secure-key-injection.md)します。

サーバーの機能:

-   [**MDEncryptData**](https://msdn.microsoft.com/library/windows/hardware/dn468756)
-   [**MDImportSessionKey**](https://msdn.microsoft.com/library/windows/hardware/dn468757)

共有関数:

-   [**CardDestroyKey**](https://msdn.microsoft.com/library/windows/hardware/dn468720)
-   [**CardGetAlgorithmProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468722)
-   [**CardGetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468728)
-   [**CardGetSharedKeyHandle**](https://msdn.microsoft.com/library/windows/hardware/dn468730)
-   [**CardProcessEncryptedData**](https://msdn.microsoft.com/library/windows/hardware/dn468732)
-   [**CardSetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468739)

クライアントの機能:

-   [**CardImportSessionKey**](https://msdn.microsoft.com/library/windows/hardware/dn468731)

## <a name="span-idsupportforrsapaddingremovaloperationsinthesmartcardspanspan-idsupportforrsapaddingremovaloperationsinthesmartcardspanspan-idsupportforrsapaddingremovaloperationsinthesmartcardspansupport-for-rsa-padding-removal-operations-in-the-smart-card"></a><span id="Support_for_RSA_Padding_Removal_Operations_in_the_Smart_Card"></span><span id="support_for_rsa_padding_removal_operations_in_the_smart_card"></span><span id="SUPPORT_FOR_RSA_PADDING_REMOVAL_OPERATIONS_IN_THE_SMART_CARD"></span>スマート カードの削除操作のパディング RSA のサポート


スマート カード ミニドライバー インターフェイスのバージョン 7 には、RSA パディングでスマート カード自体の削除操作をサポートしてスマート カード ベンダーことができます。 Base CSP または KSP の余白を削除するときに、暗号化テキスト攻撃に対する露出ができないようにします。 この機能強化には、ミニドライバーで生の RSA 暗号化解除操作の要件も削除されます。

バージョン 7 には、削除を埋め込み、内部をサポートしない古いカード (または OnCard) のサポートも提供します。 これにより、これらのカードを引き続き Base CSP または KSP が用意されている埋め込みの削除機能を使用できます。

詳細については、次を参照してください[ **PFN\_CSP\_UNPAD\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468771)と[ **CardRSADecrypt** ](https://msdn.microsoft.com/library/windows/hardware/dn468737)。この仕様で後述します。

## <a name="span-idsmartcardplugandplayspanspan-idsmartcardplugandplayspanspan-idsmartcardplugandplayspansmart-card-plug-and-play"></a><span id="Smart_Card_Plug_and_Play"></span><span id="smart_card_plug_and_play"></span><span id="SMART_CARD_PLUG_AND_PLAY"></span>スマート カードのプラグ アンド プレイ


Windows 7 コンピューターに接続されているカード リーダーにロゴ認定スマート カードが最初に挿入されると、プラグ アンド プレイ framework は Windows Update でパブリッシュされている互換性のあるミニドライバーを検索します。 ミニドライバーが見つかると、プラグ アンド プレイは自動的に Windows Update から、ミニドライバーをダウンロードして、そのコンピューターにインストールします。

詳細については、次を参照してください。[スマート カードのプラグ アンド プレイ](smart-card-plug-and-play.md)します。

## <a name="span-idcardcreatecontainerexspanspan-idcardcreatecontainerexspanspan-idcardcreatecontainerexspan-cardcreatecontainerex"></a><span id="_CardCreateContainerEx"></span><span id="_cardcreatecontainerex"></span><span id="_CARDCREATECONTAINEREX"></span> CardCreateContainerEx


この新しい API では、機能を拡張、 [ **CardCreateContainer** ](https://msdn.microsoft.com/library/windows/hardware/dn468708) API。 キー コンテナーを作成するだけでなく、コンテナーが作成されると、この関数は暗証番号 (pin) のアソシエーションを確立します。

詳細については、次を参照してください。 [ **CardCreateContainerEx** ](https://msdn.microsoft.com/library/windows/hardware/dn468709)この仕様で後述します。

## <a name="span-idnewcardcontainerpropertyforecdsaecdhkeyassociationspanspan-idnewcardcontainerpropertyforecdsaecdhkeyassociationspanspan-idnewcardcontainerpropertyforecdsaecdhkeyassociationspannew-card-container-property-for-ecdsaecdh-key-association"></a><span id="New_Card_Container_Property_for_ECDSA_ECDH_Key_Association"></span><span id="new_card_container_property_for_ecdsa_ecdh_key_association"></span><span id="NEW_CARD_CONTAINER_PROPERTY_FOR_ECDSA_ECDH_KEY_ASSOCIATION"></span>ECDSA と ECDH キーの関連付けの新しいカード コンテナーのプロパティ


この新しいコンテナーのプロパティ (ELLIPTIC Curve Diffie-hellman) キーを使用して、楕円曲線デジタル署名アルゴリズム (ECDSA) キーに関連付けます。 各 ECDSA キーは、データの暗号化と復号化に使用する ECDH キーと組み合わせて使用します。 この関連付けは、ECDSA キーを使用する場合は、暗号化を必要とするシナリオをサポートします。

ログオン証明書に ECDSA 証明書がある場合は、キャッシュされたログオン資格情報が関連付けられている ECDH キーを使用して暗号化されます。 キャッシュされたログオンの操作中にドメイン コント ローラーからのデータはユーザーのログオンに使用した ECDSA キーに関連付けられている ECDH キーを使用して復号化します。 このような状況では、コンピューターがオフラインか、ドメイン コント ローラーにアクセスできないときに、スマート カード ログオン操作を使用できます。

詳細については、CCP の説明を参照してください。\_関連付けられている\_ECDH\_後でこの仕様で [カードとコンテナーのプロパティ] でキー プロパティ。

## <a name="span-idgenericinboxminidriverthatsupportspivspanspan-idgenericinboxminidriverthatsupportspivspanspan-idgenericinboxminidriverthatsupportspivspangeneric-inbox-minidriver-that-supports-piv"></a><span id="Generic_Inbox_Minidriver_that_Supports_PIV"></span><span id="generic_inbox_minidriver_that_supports_piv"></span><span id="GENERIC_INBOX_MINIDRIVER_THAT_SUPPORTS_PIV"></span>PIV をサポートする汎用の受信トレイ ミニドライバー


Windows 7 以降、オペレーティング システムには、Personal Identity Verification (PIV) カードのエッジとデータ モデルをサポートするスマート カードで使用できる受信トレイ ジェネリック ミニドライバーが含まれています。

PIV の詳細については、「について個人アイデンティティ検証 (PIV) の連邦従業員および請負業者」の Web ページを参照してください。

Windows を特定し、受信トレイのドライバーを使用した PIV カードをペアに依存しているプロセスに関する詳細については、次を参照してください。 [Windows 受信トレイのスマート カード ミニドライバー](windows-inbox-smart-card-minidriver.md)します。

 

 





