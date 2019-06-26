---
title: カード PIN 操作
description: カード PIN 操作
ms.assetid: 7993D284-8122-4831-9C00-E53DAEB7965F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd60ebed356581de3c059cd7f45edc645bdb6c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356730"
---
# <a name="card-pin-operations"></a>カード PIN 操作


PIN が atm のテンキーの最初を使用するため、銀行業界から継承された用語。 一部の他の業界のドキュメントでは、用語のカード所有者検証 (CHV) を使用します。 データ形式は数値だけではありませんが、任意に指定できます、ユーザーが提供できる手段を自分の自由に指定されたを認識できることです。 暗証番号 (pin) のデータは、ANSI の 1 バイト文字セットに相互運用性に関する考慮事項によって制約されるように渡される値。

ユーザーの認証は、ユーザーが管理者認証のシークレットを所有する特権を持たない通常その管理者の認証から大きく異なります。 これは、データの種類の詳細については、これを使用でき、処理されるようにする方法で、深い意味があります。 このデータがいずれかに安全に漏えいの可能性なしのカードに転送またはそれ以外の場合は、完全にする必要があります管理用のシークレットは、中央機関から支援を得て、ユーザーのカードのブロックを解除するといったことをクライアント コンピューターで使用する場合短期間では、現在のトランザクション外の値を持つことがないようにします。 カードにセキュリティで保護された転送を配置するが困難なは、管理者を認証する際に PIN の使用はお勧めできません。

認証は、認証済みセッション ハイジャックから別のアプリケーションを防ぐために、トランザクション内でのみ有効です。 Deauthentication にトランザクションの終了時に自動的に発生します。

PIN を変更すると、セキュリティで保護されたトークンが無効にする必要があります。

## <a name="span-idgeneraldefinitionsspanspan-idgeneraldefinitionsspanspan-idgeneraldefinitionsspangeneral-definitions"></a><span id="General_Definitions"></span><span id="general_definitions"></span><span id="GENERAL_DEFINITIONS"></span>一般的な定義


ピンの 2 つのデータ型が定義されている: ロールに関連付けられている個々 のピンと暗証番号 (pin) を記述するための 1 つ\_PIN 識別子を持つビット マスクを使用するセット。 ユーザー名の文字列を持つ提供が中止されたをまた、PIN 識別子に変換するロール番号を導入しています。 この仕様の後半で説明する PIN の変更操作の 2 つのフラグも定義します。

```ManagedCPlusPlus
typedef     DWORD                      PIN_ID, *PPIN_ID;
typedef     DWORD                      PIN_SET, *PPIN_SET;

#define     MAX_PINS                   8

#define     ROLE_EVERYONE              0
#define     ROLE_USER                  1
#define     ROLE_ADMIN                 2

#define     PIN_SET_ALL_ROLES          0xFF
#define     CREATE_PIN_SET(PinId)      (1 << PinId)
#define     SET_PIN(PinSet, PinId)     PinSet |= CREATE_PIN_SET(PinId)
#define     IS_PIN_SET(PinSet, PinId)  (0 != (PinSet & CREATE_PIN_SET(PinId)))
#define     CLEAR_PIN(PinSet, PinId)   PinSet &= ~CREATE_PIN_SET(PinId)

#define     PIN_CHANGE_FLAG_UNBLOCK    0x01
#define     PIN_CHANGE_FLAG_CHANGEPIN  0x02
```

機能的には、現在のカード ミニドライバーのカードには、少なくとも 3 つの役割を持つすべてのカードをプロビジョニングする必要があります。ロール\_EVERYONE ロール\_ユーザー、およびロール\_管理者 各ロールは 1 つの PIN に相当\_カードの ID。 カードは、1 つだけの場合は true。 管理者ロールがあるが、その他の役割のブロックを解除できる複数の役割があります。 ただし、1 つのロールは、ファイル システムの削除などの管理者レベルの操作を実行するアクセスを制御する必要があります、これは、ロール\_管理者 さらに、ロール\_管理者ロールのブロックを解除できる必要があります\_ユーザー。 カードのファイル システムにアクセスできるように 1 つだけのユーザー ロールもあります。 3 ~ 7 の追加のロールは、省略可能なキー コンテナーにのみ関連付けることができます。

適用できる特別な考慮事項のみカード、参照してください「読み取り専用カード」後でこの仕様。

## <a name="span-idsecrettypespanspan-idsecrettypespansecrettype"></a><span id="SECRET_TYPE"></span><span id="secret_type"></span>シークレット\_型


次の列挙型では、暗証番号 (pin) の種類について説明します。

```ManagedCPlusPlus
typedef enum
{
    AlphaNumericPinType = 0,    // Regular PIN
    ExternalPinType,            // External PIN
    ChallengeResponsePinType,   // Challenge/Response PIN
    EmptyPinType                // No PIN
} SECRET_TYPE;
```

**注**暗証番号 (pin) が発生すると**シークレット\_TYPEEmptyPinType**、Windows は、PIN を要求していないも呼び出すことは**CardAuthenticatePin**または**CardAuthenticatePinEx**します。 この設定は、カード上のマテリアルに無条件のアクセスが必要な場合に便利です。



## <a name="span-idsecretpurposespanspan-idsecretpurposespansecretpurpose"></a><span id="SECRET_PURPOSE"></span><span id="secret_purpose"></span>シークレット\_目的


次の列挙型を使って、**暗証番号 (pin)\_情報**ユーザー情報の目的の PIN の目的を説明するデータ構造。

```ManagedCPlusPlus
typedef enum
{
    AuthenticationPin,      // Authentication PIN
    DigitalSignaturePin,    // Digital Signature PIN
    EncryptionPin,          // Encryption PIN
    NonRepudiationPin,      // Non Repudiation PIN
    AdministratorPin,       // Administrator PIN
    PrimaryCardPin,
    UnblockOnlyPin          // Unblocking other PINs
} SECRET_PURPOSE;
```

Windows では、列挙値を使用して、PIN が要求される現在どのカードを説明するユーザーに適切なメッセージを表示します。 どのシークレットを完全に制御する、ミニドライバー\_を使用する型。 サンプルのコンテキストの文字列を含む PIN プロンプト ダイアログ ボックスの例を次に示します。

![ピン留めする ダイアログ ボックス](images/pinbox.png)

最初の文字列の図 (入力ピン留めします。 登録。BaseRSASmartcardLogon") は、アプリケーションのコンテキストを提供する、呼び出し元アプリケーションによって提供されます。 アプリケーション コンテキストの文字列が存在しない場合、ダイアログ ボックスには、標準のテキストが表示されます。

2 番目の文字列 (「を入力してください、認証のピン留めする」) によって**シークレット\_目的**次の方法のいずれかで。

-   既定のコンテキスト文字列

    既定では、Base CSP は、適切にローカライズされて次の定義済み文字列を表示します。

    |                     |                                                  |
    |---------------------|--------------------------------------------------|
    | AuthenticationPin   | 「認証 PIN を入力してください」          |
    | DigitalSignaturePin | 「デジタル署名の PIN を入力してください」       |
    | EncryptionPin       | 「、暗号化の PIN を入力してください」              |
    | NonRepudiationPin   | 「、否認暗証番号 (pin) を入力してください」         |
    | AdministratorPin    | 「管理者 PIN を入力してください」           |
    | PrimaryCardPin      | 「、PIN を入力してください」                         |
    | UnblockOnlyPin      | 「ユーザー暗証番号のブロックを解除する PIN を入力してください」 |



-   カスタム文字列

    開発者は、ミニドライバーのレジストリ キーの次のレジストリ値のカスタム文字列を設定して既定のコンテキストの文字列を上書きできます (HKLM\\ソフトウェア\\ソフトウェア\\Microsoft\\暗号化\\Calais\\スマート カード\\XYZ、XYZ はカードのミニドライバーの名前)。

    定義済みのコンテキストの文字列を上書きするには、カスタムの文字列で、ミニドライバーのレジストリ キーにレジストリ文字列値を追加します。 キーの名前を設定する**シークレット\_目的**0x80000100 の最初のメンバーに対応すると、定義済みのコンテキストの文字列がオーバーライドされる**シークレット\_型**と以降。 一部、またはすべてのコンテキスト文字列、1 つの文字列を上書きすることはできません。

    文字列の値は、次の形式に従う必要があります。

    ``` syntax
    “LangID,xxxx;LangID,xxxxx”
    ```

    **注**カスタム文字列を囲む引用符が適切に処理しないと、文字列内の特殊文字の解析を回避するに依存する必要があります。




**注**最初のカスタム文字列の中で同じロケールの結果が集荷の 2 つの異なるカスタム文字列を含むです。




3 番目の文字列 ("デジタル署名ピン留めする) ダイアログ ボックスでは、定義済みの文字列によって決定される、**シークレット\_目的**値、 **PIN\_情報**データ構造体。

**UnblockOnlyPin**、本来の目的は、ユーザー暗証番号のブロックを解除します。 他の目的この PIN を使用しない必要があります。

## <a name="span-idpincachepolicytypespanspan-idpincachepolicytypespan-pincachepolicytype"></a><span id="_PIN_CACHE_POLICY_TYPE"></span><span id="_pin_cache_policy_type"></span> PIN\_キャッシュ\_ポリシー\_型


次の列挙型では、暗証番号 (pin) のキャッシュはこの PIN に関連するポリシーについて説明します。

```ManagedCPlusPlus
typedef enum
{
    PinCacheNormal = 0,
    PinCacheTimed,
    PinCacheNone,
    PinCacheAlwaysPrompt
} PIN_CACHE_POLICY_TYPE;
```

次の表では、3 つの異なるキャッシュ モード時に、Base CSP の機能について説明します。

| キャッシュ モード               | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PinCacheNormal**       | このモードの場合、PIN は、ログオン ID ごとのプロセスごとの Base CSP によってキャッシュされます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **PinCacheTimed**        | このモードでは、(値がで指定された秒数) の指定された期間の後に、PIN が無効になります。 これは、PIN がキャッシュに追加されたときに、タイムスタンプを記録し、このタイムスタンプと、暗証番号 (pin) がアクセスされるときの時刻を検証することによって実装されていました。 つまり、暗証番号 (pin) 可能性がある、指定されたタイムスタンプよりも長くキャッシュに在住が有効期限が切れた後は使用されません。 PIN は、保護されるようにするメモリ内で暗号化されます。                                                                                                                |
| **PinCacheNone**         | PIN はキャッシュされることはできません、Base CSP は、暗証番号 (pin) をことはありません、キャッシュに追加します。 Base CSP または KSP がで呼び出された[ **CryptSetProvParam** ](https://docs.microsoft.com/windows/desktop/api/wincrypt/nf-wincrypt-cryptsetprovparam)暗証番号 (pin) の検証のため、カードに送信されたがキャッシュされていない PIN を設定します。 つまり、後続の操作は、Base CSP トランザクションのタイムアウトの有効期限が切れる前に発生する必要があります。                                                                                                                                                                                                                  |
| **PinCacheAlwaysPrompt** | 異なり**PinCacheNone**このキャッシュ モードが設定されている場合、Base CSP トランザクションのタイムアウトは適用されません。 PIN がユーザーから収集し、認証が必要な各呼び出しの前に確認のため、カードに送信されます。 呼び出す[ **CryptSetProvParam** ](https://docs.microsoft.com/windows/desktop/api/wincrypt/nf-wincrypt-cryptsetprovparam)と[ **NcryptSetProperty** ](https://docs.microsoft.com/windows/desktop/api/ncrypt/nf-ncrypt-ncryptsetproperty)の PIN の設定のエラーが返されます\_なしの成功検証と、暗証番号 (pin) のキャッシュです。 つまり、呼び出しが認証を必要とする場合に、サイレントのコンテキストを使用するアプリケーションからの呼び出しが失敗します。 |



**注**PIN がキャッシュされていない場合、Windows ログオンが正常に動作しない可能性があります。 この動作は仕様による結果です。 暗証番号 (pin) のキャッシュ モードを以外の任意の値を設定するときの慎重に検討の指定、 **PinCacheNormal**します。



## <a name="span-idpincachepolicyspanspan-idpincachepolicyspan-pincachepolicy"></a><span id="_PIN_CACHE_POLICY"></span><span id="_pin_cache_policy"></span> PIN\_キャッシュ\_ポリシー


暗証番号 (pin) のキャッシュ ポリシー構造体には、暗証番号 (pin) のキャッシュ ポリシーを説明する情報が含まれています。 これには、この暗証番号 (pin) のキャッシュ ポリシーに関連付けられている情報に加え、暗証番号 (pin) キャッシュの種類について説明します。 ポリシーが示されている場合、この関連付けられている情報の例は、暗証番号 (pin) のキャッシュのタイムアウト値になります**PinCacheTimed**します。

```ManagedCPlusPlus
#define      PIN_CACHE_POLICY_CURRENT_VERSION   6

typedef struct _PIN_CACHE_POLICY
{
    DWORD                   dwVersion;
    PIN_CACHE_POLICY_TYPE   PinCachePolicyType;
    DWORD                   dwPinCachePolicyInfo;
} PIN_CACHE_POLICY, *PPIN_CACHE_POLICY;
```

## <a name="span-idpininfospanspan-idpininfospanpininfo"></a><span id="PIN_INFO"></span><span id="pin_info"></span>PIN\_情報


暗証番号 (pin) のオブジェクトの構造には、暗証番号 (pin) を説明する情報が含まれています。 これには、このターゲットの暗証番号 (pin)、およびキャッシュ ポリシーの PIN のブロックを解除する PIN が許可されている PIN の種類について説明します。 Base CSP または KSP によって暗証番号 (pin) 情報構造体を取得した後は、データ ファイルのキャッシュ方法のようなデータ キャッシュにキャッシュする必要があります。

```ManagedCPlusPlus
#define      PIN_INFO_REQUIRE_SECURE_ENTRY       1

typedef struct _PIN_INFO
{
    DWORD                   dwVersion;
    SECRET_TYPE             PinType;
    SECRET_PURPOSE          PinPurpose;
    PIN_SET                 dwChangePermission;
    PIN_SET                 dwUnblockPermission;
    PIN_CACHE_POLICY        PinCachePolicy;
    DWORD                   dwFlags;
} PIN_INFO, *PPIN_INFO;
```

**DwUnblockPermission**メンバーがどのピンを表すビット マスクは、PIN のブロックを解除する権限を持っています。 アクセス許可は、指定した Pin のビットごとの 'または' に基づいています。 ブロック解除操作の場合、自己参照カード ミニドライバーを無視します。 ロール\_update 権限のビットマスク 0x00000100 のユーザーが必要があります。 これは、ロールによって解除できることを意味\_管理者 ロール\_管理者は、0x00000000 の update 権限を持ちます。 つまり、ブロックを解除とできません。

**DwFlags**メンバーには、暗証番号 (pin) フラグが含まれています。 現時点では、1 つのみのフラグが定義されます。PIN\_情報\_REQUIRE\_SECURE\_エントリ。 このフラグは、セキュリティで保護されたデスクトップは、PIN の入力に必要かどうかを Base CSP または KSP に示します。

**注**は、この構造体を使用してロールを付与するして\_EVERYONE のアクセス許可を変更または PIN のブロックを解除します。 これには、しないでし、ロールを許可する API のミニドライバーのメカニズムは提供されません\_EVERYONE を変更または PIN のブロックを解除します。











