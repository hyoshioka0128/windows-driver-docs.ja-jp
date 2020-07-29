---
title: カード PIN 操作
description: カード PIN 操作
ms.assetid: 7993D284-8122-4831-9C00-E53DAEB7965F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 341451de05573a4eec9ae4368d0073465eca7242
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264457"
---
# <a name="card-pin-operations"></a>カード PIN 操作


ATM コンピューターのテンキーで最初に使用されたため、PIN という用語は銀行業界から継承されています。 他の業界のドキュメントでは、カード所有者の確認 (CHV) を使用しています。 データ形式は数値ではなく、ユーザーが自由に指定できるようにすることができるということを理解しています。 ピンデータとして渡される値は、ANSI 1 バイト文字セットに対する相互運用性に関する考慮事項によって制限されます。

ユーザーの認証は、管理者の認証とは大きく異なります。ユーザーは通常、管理者認証のシークレットを保持する特権を持っていません。 これには、どのような種類のデータを使用できるか、およびどのように処理されるかに関して多くの影響があります。 中央機関からの支援を受けたユーザーのカードのブロック解除などを行うために、クライアントコンピューターで管理シークレットを使用する場合、このデータは開示されないように安全にカードに転送するか、または現在のトランザクションの外部に値がないように完全に一時的にする必要があります。 セキュリティで保護された転送をカードに配置するのが難しいのは、PIN を使用して管理者を認証することが推奨されないためです。

認証は、トランザクション内でのみ有効です。これにより、別のアプリケーションが認証されたセッションをハイジャックするのを防ぐことができます。 トランザクションの終了時に、deauthentication が自動的に行われます。

PIN を変更すると、セキュリティで保護されたトークンが無効になります。

## <a name="span-idgeneral_definitionsspanspan-idgeneral_definitionsspanspan-idgeneral_definitionsspangeneral-definitions"></a><span id="General_Definitions"></span><span id="general_definitions"></span><span id="GENERAL_DEFINITIONS"></span>一般的な定義


Pin には2つのデータ型が定義されています。1つは、 \_ pin 識別子を持つビットマスクに使用される、ロールとピンセットに関連付けられている個々の pin を記述するためのものです。 また、ユーザー名の文字列を保持し、PIN 識別子に変換するロール番号を導入しました。 また、この仕様の後半で説明する PIN 変更操作の2つのフラグを定義します。

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

現在のカードミニドライバーカードと機能的に同等のものにするには、すべてのカードが少なくとも3つのロール (ロール \_ 全員、ロール \_ ユーザー、ロール管理者) を使用してプロビジョニングされている必要があります。 \_ 各ロールは、カードの1つの PIN ID に相当 \_ します。 カードには真の管理者ロールが1つだけ存在しますが、他のロールのブロックを解除できるロールは複数存在する可能性があります。 ただし、ファイルシステムの削除などの管理者レベルの操作を実行するためのアクセスを制御する必要があるのは、ロール管理者だけです \_ 。 また、ロール \_ 管理者は、ロールユーザーのブロックを解除できる必要があり \_ ます。 カードのファイルシステムへのアクセス権を付与するユーザーロールは1つだけです。 追加のロール 3 ~ 7 は省略可能で、キーコンテナーにのみ関連付けることができます。

読み取り専用カードに適用できる特別な考慮事項については、この仕様で後述する「読み取り専用カード」を参照してください。

## <a name="span-idsecret_typespanspan-idsecret_typespansecret_type"></a><span id="SECRET_TYPE"></span><span id="secret_type"></span>シークレットの \_ 種類


次の列挙体は、PIN の種類を示しています。

```ManagedCPlusPlus
typedef enum
{
    AlphaNumericPinType = 0,    // Regular PIN
    ExternalPinType,            // External PIN
    ChallengeResponsePinType,   // Challenge/Response PIN
    EmptyPinType                // No PIN
} SECRET_TYPE;
```

**メモ** PIN **SECRET \_ TYPEEmptyPinType**が発生した場合、Windows は pin を要求したり、 **CardAuthenticatePin**または**CardAuthenticatePinEx**を呼び出したりしません。 この設定は、カード上のマテリアルへの無条件アクセスが必要な場合に便利です。



## <a name="span-idsecret_purposespanspan-idsecret_purposespansecret_purpose"></a><span id="SECRET_PURPOSE"></span><span id="secret_purpose"></span>シークレットの \_ 目的


次の列挙体は、ユーザー情報の目的で PIN の目的を示すために、 **pin \_ 情報**のデータ構造で使用されます。

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

Windows は列挙値を使用して、現在要求されているカード PIN を説明する適切なメッセージをユーザーに表示します。 ミニドライバーは、使用するシークレットの種類を完全に制御し \_ ます。 次に示すのは、サンプルコンテキスト文字列を含む [PIN プロンプト] ダイアログボックスの図です。

![[ピン留めする] ダイアログボックス](images/pinbox.png)

図の最初の文字列 (「PIN の入力」を入力します。 : BaseRSASmartcardLogon ") の登録は、アプリケーションコンテキストを提供するために、呼び出し元のアプリケーションによって提供されます。 アプリケーションコンテキスト文字列が存在しない場合、ダイアログボックスには標準のテキストが表示されます。

2番目の文字列 ("認証 PIN を入力してください") は、次のいずれかの方法で**シークレットの \_ 目的**によって決定されます。

-   既定のコンテキスト文字列

    既定では、ベース CSP は、適切にローカライズされた次の定義済みの文字列を表示します。

    | 文字列名        |  String                                          |
    |---------------------|--------------------------------------------------|
    | AuthenticationPin   | "認証 PIN を入力してください。"          |
    | DigitalSignaturePin | "デジタル署名の PIN を入力してください。"       |
    | EncryptionPin       | "暗号化 PIN を入力してください。"              |
    | NonRepudiationPin   | "否認不可の PIN を入力してください。"         |
    | アドミニストレーターの Pin    | "管理者の PIN を入力してください。"           |
    | PrimaryCardPin      | "PIN を入力してください。"                         |
    | UnblockOnlyPin      | "ユーザー暗証番号のブロックを解除するには、PIN を入力してください。" |



-   カスタム文字列

    開発者は、ミニドライバーのレジストリキーの次のレジストリ値にカスタム文字列を設定して、既定のコンテキスト文字列を上書きできます (HKLM \\ software \\ software \\ Microsoft \\ Cryptography \\ CALAIS \\ スマートカード \\ xyz、xyz はカードミニドライバーの名前です)。

    定義済みのコンテキスト文字列をオーバーライドするには、ミニドライバーのレジストリキーに、カスタム文字列を使用してレジストリ文字列値を追加します。 秘密の** \_ 目的**として定義済みのコンテキスト文字列を上書きするキーの名前を設定します。**シークレット \_ 型**の最初のメンバーに対応する0x80000100 を使用します。 1つの文字列、一部、またはすべてのコンテキスト文字列をオーバーライドすることはできません。

    文字列の値は、次の形式に従う必要があります。

    ``` syntax
    “LangID,xxxx;LangID,xxxxx”
    ```

    **メモ** カスタム文字列を囲む引用符は適切に処理されないため、文字列内の特殊文字の解析を防ぐために依存しないようにする必要があります。




**メモ** 同じロケールに2つの異なるカスタム文字列を含めると、最初のカスタム文字列が取得されます。




ダイアログボックスの3番目の文字列 ("デジタル署名 PIN") は、 **PIN \_ 情報**のデータ構造の**秘密の \_ 目的**の値によって決定される定義済みの文字列です。

**UnblockOnlyPin**の目的は、ユーザー PIN のブロックを解除することです。 この PIN は、他の目的には使用しないでください。

## <a name="span-id_pin_cache_policy_typespanspan-id_pin_cache_policy_typespan-pin_cache_policy_type"></a><span id="_PIN_CACHE_POLICY_TYPE"></span><span id="_pin_cache_policy_type"></span>PIN \_ キャッシュ \_ ポリシーの \_ 種類


次の列挙は、この PIN に関連付けられるピンキャッシュポリシーを示しています。

```ManagedCPlusPlus
typedef enum
{
    PinCacheNormal = 0,
    PinCacheTimed,
    PinCacheNone,
    PinCacheAlwaysPrompt
} PIN_CACHE_POLICY_TYPE;
```

次の表では、ベース CSP が3つの異なるキャッシュモードにどのように作用するかを説明します。

| キャッシュモード               | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **PinCacheNormal**       | このモードでは、PIN はログオン ID ごとのプロセスごとのベース CSP によってキャッシュされます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **PinCacheTimed**        | このモードでは、指定された期間 (秒単位の値) の後に PIN が無効になります。 これは、PIN がキャッシュに追加されたときにタイムスタンプを記録し、このタイムスタンプと PIN がアクセスされた時間を確認することによって実装されました。 これは、PIN が指定されたタイムスタンプよりも長いキャッシュ内に存在する可能性がありますが、有効期限が切れた後は使用されないことを意味します。 PIN は、保護された状態を維持するために、メモリ内で暗号化されます。                                                                                                                |
| **PinCacheNone**         | PIN をキャッシュできない場合、基本 CSP は PIN をキャッシュに追加しません。 PIN を設定するために[**CryptSetProvParam**](https://docs.microsoft.com/windows/desktop/api/wincrypt/nf-wincrypt-cryptsetprovparam)を使用して Base CSP/KSP を呼び出すと、pin は検証のためにカードに送信されますが、キャッシュされません。 これは、基本 CSP トランザクションのタイムアウトの期限が切れる前に、後続の操作が行われる必要があることを意味します。                                                                                                                                                                                                                  |
| **Pincachealways Prompt** | **Pincachenone**とは異なり、このキャッシュモードが設定されている場合、Base CSP トランザクションのタイムアウトは適用されません。 PIN はユーザーから収集され、認証を必要とする各呼び出しの前に検証のためにカードに送信されます。 Pin の確認とキャッシュを行わずに、PIN を設定するための[**CryptSetProvParam**](https://docs.microsoft.com/windows/desktop/api/wincrypt/nf-wincrypt-cryptsetprovparam)と[**ncryptsetproperty**](https://docs.microsoft.com/windows/desktop/api/ncrypt/nf-ncrypt-ncryptsetproperty)の呼び出しでエラーが発生し \_ ます。 これは、呼び出しで認証が必要な場合に、サイレントコンテキストを使用するアプリケーションからの呼び出しが失敗することを意味します。 |



**メモ** PIN がキャッシュされていない場合、Windows ログオンが正しく機能しない可能性があります。 この動作は仕様です。 したがって、PIN キャッシュモードを**PinCacheNormal**以外の値に設定する場合は、慎重に検討する必要があります。



## <a name="span-id_pin_cache_policyspanspan-id_pin_cache_policyspan-pin_cache_policy"></a><span id="_PIN_CACHE_POLICY"></span><span id="_pin_cache_policy"></span>PIN \_ キャッシュ \_ ポリシー


PIN キャッシュポリシーの構造には、PIN キャッシュポリシーを説明する情報が含まれています。 この PIN キャッシュポリシーに関連付けられている情報に加えて、PIN キャッシュの種類についても説明します。 この関連情報の例として、ポリシーが**Pincachetimed**を示す場合の PIN キャッシュのタイムアウト値があります。

```ManagedCPlusPlus
#define      PIN_CACHE_POLICY_CURRENT_VERSION   6

typedef struct _PIN_CACHE_POLICY
{
    DWORD                   dwVersion;
    PIN_CACHE_POLICY_TYPE   PinCachePolicyType;
    DWORD                   dwPinCachePolicyInfo;
} PIN_CACHE_POLICY, *PPIN_CACHE_POLICY;
```

## <a name="span-idpin_infospanspan-idpin_infospanpin_info"></a><span id="PIN_INFO"></span><span id="pin_info"></span>PIN \_ 情報


ピン留めオブジェクトの構造には、PIN を説明する情報が含まれています。 Pin の種類について説明します。 pin は、このピンのブロックを解除できます。また、pin のキャッシュポリシーを使用します。 基本 CSP/KSP によって取得された PIN 情報の構造は、データファイルのキャッシュと同様にデータキャッシュにキャッシュする必要があります。

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

**DwUnblockPermission**メンバーは、pin のブロックを解除するアクセス許可が付与されている pin を示すビットマスクです。 このアクセス許可は、指定されたピンのビットごとの ' or ' に基づいています。 ブロック解除操作の場合、カードミニドライバーは自己参照を無視する必要があります。 ロールユーザーには、 \_ 更新のアクセス許可である、0x00000100 のビットマスクがあります。 これは、ロール管理者がブロックを解除できることを意味 \_ します。 ロール \_ 管理者。0x00000000 の更新権限があります。 これは、ブロックを解除できないことを意味します。

**DwFlags**メンバーには、PIN フラグが含まれています。 現在、1つのフラグのみが定義されています。 PIN 情報には \_ \_ \_ セキュリティで保護されたエントリが必要 \_ です。 このフラグは、PIN の入力にセキュリティで保護されたデスクトップが必要かどうかを Base CSP/KSP に示します。

**メモ** この構造を使用して、ロール \_ のすべてのユーザーに PIN の変更またはブロック解除のアクセス許可を与えることができます。 これは推奨されません \_ 。ロール全員が PIN を変更またはブロック解除することを許可するメカニズムはミニドライバー API には用意されていません。











