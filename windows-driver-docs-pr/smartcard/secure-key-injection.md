---
title: セキュリティで保護されたキーの挿入
description: セキュリティで保護されたキーの挿入
ms.assetid: 21F8ED59-B04C-40D3-AEED-015890798215
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56843d10d3555f7b21f53785f7304f95e0eda6d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580327"
---
# <a name="secure-key-injection"></a>セキュリティで保護されたキーの挿入


セキュリティで保護されたキーの挿入は、信頼されていないクライアントからスマート カードへのサーバー アプリケーションから暗号化された転送される機密情報のサポートを提供します。 適切に機能するセキュリティで保護されたキー挿入の次の手順が発生する必要があります。

1.  暗号化キーの確立:

    1.  サーバーとクライアントのスマート カードの間で共有対称キーを使用します。
    2.  サーバー上の一時対称セッション キーを生成して、スマート カードをインポートします。 セッション キーは、スマート カードに生成された対応する秘密キーを持つ公開キーで暗号化する必要があります。
    3.  セッション キーを共有対称キーから派生させます。 詳細については、[ **CardGetSharedKeyHandle**](https://msdn.microsoft.com/library/windows/hardware/dn468730)を参照してください。
    4.  DH キーの派生を使用します。

2.  サーバー上のデータの暗号化:

    1.  データには、PIN などの認証データは、可能性があります。
    2.  データは、非対称キー ペア (RSA/ECC など) になります。

3.  クライアントにスマート カード内のデータの復号化します。

次の図は、キーを生成し、安全にキー信頼境界を越えて、クライアントに転送するサーバー アプリケーションを示します。 キーが受信されると、クライアントはこれをスマート カードをインポートします。 最後の手順として、キーは、CA にインポート アーカイブします。 サーバー アプリケーションと、スマート カードの間に、暗号化されたチャネルが存在する必要があり、クライアント アプリケーション/ミニドライバーは、暗号化されたデータにアクセスすることはできません。

![スマート カードによるセキュリティで保護されたキーの挿入中にサーバー クライアントとの対話の概要](images/seckeyinj.png)

手順 2. でキーを暗号化するには、サーバーとスマート カード、共有対称キーが必要です。

セキュリティで保護されたキーの挿入を実行するときに、独自の形式を使用する既存のカードを対応するために、ミニドライバー読み込めるサーバー側で存在しているカードがないです。 ミニドライバーは、メッセージの形式し、し、最後に、暗号化、メッセージを復号化するクライアントで実行されている同じミニドライバーをできます。

次の図は、サーバー/クライアント キーのミニドライバーとアーカイブの概要を示します。

![サーバー/クライアント キーのミニドライバーとアーカイブの概要](images/seckeyarch.png)

## <a name="span-idcardkeyhandlespanspan-idcardkeyhandlespanspan-idcardkeyhandlespancard-key-handle"></a><span id="Card_Key_Handle"></span><span id="card_key_handle"></span><span id="CARD_KEY_HANDLE"></span>キー ハンドルのカード


対称キー、カードを扱うとき\_キー\_ハンドルは、キー ハンドルを渡すために使用する必要があります。

``` syntax
typedef ULONG_PTR  CARD_KEY_HANDLE;
```

## <a name="span-idnocardmodespanspan-idnocardmodespanspan-idnocardmodespan-no-card-mode"></a><span id="_No_Card_Mode"></span><span id="_no_card_mode"></span><span id="_NO_CARD_MODE"></span> カード モードなし


書式を設定して、信頼されていないクライアントにインストールされている同じミニドライバーを使用してデータを暗号化するサーバー アプリケーションを容易に[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)を必要としないモードで呼び出すことができます存在するカードです。 このモードが有効で、次のフラグを設定して、 *dwFlags*パラメーターの**CardAcquireContext**します。

``` syntax
#define CARD_SECURE_KEY_INJECTION_NO_CARD_MODE  0x1
```

この設定によって、 [ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)がいずれかのカード リーダーにします。 つまり、ATR のフィールド、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)は塗りつぶされていないと**hSCard**と**hSCardCtx**が 0 に設定します。

このフラグが設定されている場合、ミニドライバーは、次の関数呼び出しのみを受け入れることができます。

-   [**MDImportSessionKey**](https://msdn.microsoft.com/library/windows/hardware/dn468757)
-   [**MDEncryptData**](https://msdn.microsoft.com/library/windows/hardware/dn468756)
-   [**CardGetSharedKeyHandle**](https://msdn.microsoft.com/library/windows/hardware/dn468730)
-   [**CardGetAlgorithmProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468722)
-   [**CardDestroyKey**](https://msdn.microsoft.com/library/windows/hardware/dn468720)
-   [**CardGetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468728)
-   [**CardSetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468739)
-   [**CardProcessEncryptedData**](https://msdn.microsoft.com/library/windows/hardware/dn468732)

## <a name="span-idusecasescenarioforsecurekeyinjectionspanspan-idusecasescenarioforsecurekeyinjectionspanspan-idusecasescenarioforsecurekeyinjectionspanuse-case-scenario-for-secure-key-injection"></a><span id="Use_Case_Scenario_for_Secure_Key_Injection"></span><span id="use_case_scenario_for_secure_key_injection"></span><span id="USE_CASE_SCENARIO_FOR_SECURE_KEY_INJECTION"></span>ユース ケース シナリオは、セキュリティで保護されたキーの挿入


このシナリオの例では、クライアント アプリケーションは、スマート カードの所有者に代わってサーバーで実行されている CA アプリケーションから、証明書を発行することを要求します。 CA には、キーのアーカイブも必要です。 参照してくださいセクション内の脚注にセキュリティで保護されたキーの挿入ガイダンスについては、非対称キー ペアを使用して一時対称セッション キーを確立します。

ユーザー キーがサーバー側で生成され、アーカイブ、セキュリティで保護されたキーの挿入関数を使用して、ユーザーのスマート カードに挿入されます。 次の図は、プロセスを示します。

![キーの生成と挿入のためのプロセス](images/skiusecase.png)

このシナリオはに基づいて、非対称キーで暗号化された対称セッション キーをインポートし、後続のキーのラップのこの対称キーを使用します。

次の手順は、前の図に示すように、プロセスを説明します。

1.  クライアント アプリケーションでは、サーバーで実行されている CA アプリケーションから新しい証明書を要求します。
2.  クライアントの要求を受信した場合は、キー回復証明書テンプレートが構成されているサーバー アプリケーションが検出されます。 その結果、サーバー アプリケーションは、セキュリティで保護されたキー挿入プロトコルを開始します。
3.  クライアント アプリケーションの呼び出し[ **CardGetProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468729) CP の\_キー\_インポート\_次の検出をサポートします。

    -   かどうか、カードでは、セキュリティで保護されたキーの挿入をサポートしています。
    -   対称キーのインポートの方法がサポートされています。
    -   どのようなアルゴリズムがサポートされています。

4.  非対称のメカニズムを通じてキーの挿入をサポートしているクライアント アプリケーションに、ミニドライバーを示します (カード\_キー\_インポート\_非対称\_KEYEST)。
5.  クライアント アプリケーションは、任意のコンテナーのキーのインポートに便利ですが、スマート カードのコンテナーのマップ ファイルを検索します。 見つからない場合、クライアント アプリケーションが呼び出す[ **CardCreateContainer** ](https://msdn.microsoft.com/library/windows/hardware/dn468708)新しいキー ペアを生成します。
6.  ミニドライバーは、スマート カード キー ペアを作成するように指示します。
7.  スマート カードは、キーが作成されたら、ミニドライバーにキーを返します。
8.  ミニドライバーは、キーが生成されたこと、クライアント アプリケーションを示す値を返します。
9.  これで、クライアント アプリケーションを呼び出す[ **CardGetContainerInfo** ](https://msdn.microsoft.com/library/windows/hardware/dn468725)手順 6 で作成されたキーのペアの公開キーをエクスポートします。
10. カードのミニドライバーは、カードを使用する公開キーを返すように指示します。
11. カードはカードから公開キー (K1) を抽出し、ミニドライバーに返します。
12. ミニドライバーは、クライアント アプリケーションに K1 を返します。
13. クライアント アプリケーションの呼び出し[ **CardGetProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468729)カードをサポートする対称アルゴリズムを列挙するためにも同様列挙パディング方式 K1 で使用できます。
14. ミニドライバーは、アルゴリズムとサポートされているパディング モードを返します。
15. クライアント アプリケーションでは、対称キー アルゴリズムと、カードをサポートするパディング モードを示す情報と共に、サーバー アプリケーションに戻る K1 を送信します。
16. カードをサポートするアルゴリズムのいずれかを使用してでは、サーバー アプリケーションは、対称キー (S1) を生成します。 対称キーの S1 が K1 を使用して暗号化し、クライアント アプリケーションに返されます。 サーバー アプリケーションでは、暗号化アルゴリズムについての情報も返されます、埋め込みの型は、S1 の暗号化に使用されました。
17. クライアント アプリケーションの呼び出し[ **CardImportSessionKey** ](https://msdn.microsoft.com/library/windows/hardware/dn468731)を BLOB に暗号化されたキー データが BLOB を復号化に使用するには、K1 およびパディング情報への参照と共に使用します。

    キーのデータの Blob の詳細については、[ **BCRYPT\_キー\_データ\_BLOB\_ヘッダー**](https://msdn.microsoft.com/library/windows/desktop/aa375524)を参照してください。

18. ミニドライバーは、暗号化された BLOB データを復号化用のスマート カードに渡します。
19. 対称キーの暗号化を解除した後、スマート カード ミニドライバーに対称キーへの参照を返します。
20. ミニドライバーは、対称キーのクライアント アプリケーションにキー ハンドルを返します。
21. クライアント アプリケーションは、対称キーがインポートされていること、サーバー アプリケーションから受信確認を送信します。
22. サーバー アプリケーションは、サーバー側のミニドライバーを呼び出して S1 をインポートする[ **MDImportSessionKey**](https://msdn.microsoft.com/library/windows/hardware/dn468757)します。
23. サーバー側のミニドライバーは、S1 に正常にインポートされたことを示す成功を返します。
24. サーバー アプリケーションでは、非対称キー ペア (K2) を生成します。 K2 は呼び出すことによって、サーバー側のミニドライバーに送信される[ **MDEncryptData**](https://msdn.microsoft.com/library/windows/hardware/dn468756)します。 サーバー アプリケーションが、IV とモードの組み合わせを生成し、サーバー側のミニドライバーを呼び出すことによってこの情報を設定[ **CardSetKeyProperty**](https://msdn.microsoft.com/library/windows/hardware/dn468739)します。
25. サーバー側のミニドライバーは、S1 を使用して K2 を暗号化し、サーバー アプリケーションに暗号化された K2 を返します。
26. サーバー アプリケーションでは、暗号化に関連するすべての情報と共に、クライアント アプリケーションを encryptedK2 を送信します。 これには、IV およびモードの情報のチェーンが含まれます。
27. クライアント アプリケーションの呼び出し[ **CardSetKeyProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468739) S1 で使用するにはどのような IV とチェーン モード、ミニドライバーに指示します。 クライアント アプリケーションから呼び出す[ **CardProcessEncryptedData** ](https://msdn.microsoft.com/library/windows/hardware/dn468732)次のデータ。

    -   暗号化されたキー データ K2 を格納する BLOB。
    -   キーは、カードのデータの暗号化を解除して、キーを作成できるように、S1 に参照します。

28. ミニドライバーは新しいキー コンテナーを準備するために必要な手順を実行し、スマート カードへの暗号化キー データ BLOB を提供します。
29. スマート カードは、K2 S1 を使用して復号化し、K2 用に新しいキー コンテナーを生成します。 カードは、キーがインポートされていることを示す成功を返します。
30. 成功を返します、ミニドライバー [ **CardProcessEncryptedData**](https://msdn.microsoft.com/library/windows/hardware/dn468732)します。
31. クライアント アプリケーションは成功を返し、プロセスが完了します。

 

 





