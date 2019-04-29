---
title: スマート カード ミニドライバーの概要
description: スマート カード ミニドライバーの概要
ms.assetid: B5047C79-F74E-44FA-ADE5-8716ABC9EB79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2f48eef2d68b5fb6ae801fe8834a2e4e7121aa1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390911"
---
# <a name="smart-card-minidriver-overview"></a>スマート カード ミニドライバーの概要


特定のカード ミニドライバーは、Base CSP または KSP で最下位の論理インターフェイス層です。 このミニドライバーは、Base CSP または KSP を使用し、SCRM を使用して、アプリケーションが特定の種類のカードと直接対話します。

カードのミニドライバーは、この仕様で定義されている特定の Api のセットをエクスポートする DLL です。 カードのミニドライバーを呼び出すたびにへのポインターが含まれています、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)コンテキスト情報を提供する構造体。 このコンテキスト情報は、上位レイヤーとカードのミニドライバー間の通信を容易にするために使用される関数ポインターのいくつかの状態情報だけでなく、テーブルを提供します。

このコンテキストの構造体の詳細については、次を参照してください。 [ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)します。

## <a name="span-idrelateddocumentspanspan-idrelateddocumentspanspan-idrelateddocumentspanrelated-document"></a><span id="Related_Document"></span><span id="related_document"></span><span id="RELATED_DOCUMENT"></span>関連ドキュメント


*Cardmod.h* C ヘッダー ファイルは、この仕様に関連する追加の情報を提供します。 このファイルには、Microsoft のスマート カード ミニドライバーの API を指定する関数プロトタイプと構造体が含まれています。 この API は使用を通じて、Microsoft 暗号化サービス プロバイダーの開発キット (CPDK) です。

## <a name="span-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspanspan-idgeneraldesignguidelinesspangeneral-design-guidelines"></a><span id="General_Design_Guidelines"></span><span id="general_design_guidelines"></span><span id="GENERAL_DESIGN_GUIDELINES"></span>一般的なデザイン ガイドライン


-   カードのミニドライバーは、DLL として配布する必要があります。
-   各カードに固有の操作として明記を除く、1 つのアトミック トランザクションを実装する必要があります。
-   標準化されたマクロ レベルの操作のセットを実装する必要があります。
-   論理のカードのファイル システム オブジェクトは、その物理的な場所にマップする必要があります。
-   この新しいモデルに基づいたカードのカードに格納されているすべてのファイルを動的に拡張できる必要があります。 カードは読み取り専用であり、このガイドラインに従うことはできませんが、ミニドライバーは、この仕様に記載された読み取り専用のカードに関する特定のガイドラインに従う必要があります。
-   ミニドライバーは、CPDK から定義をインポートします。 ミニドライバーのヘッダー ファイル (*Cardmod.h*) が含まれています*Bcrypt.h*この目的のためです。 実装では、ミニドライバーをコンパイルするため、Microsoft Visual Studio プロジェクトの設定を使用して、この依存関係を解決する必要があります。
-   プラグインまたはドライバーの保護されたプロセスの要件

    -   保護されたプロセスとして正しく読み込むには、LSA のプラグイン、またはドライバーには、次の条件を満たす必要があります。

        -   署名の検証

            o 保護モードが必要ですすべてのプラグインに読み込まれている、LSA はマイクロソフトの署名とデジタル署名する必要があります。 そのため、任意符号なし、または 3 番目の利用者署名プラグインの LSA の読み込みに失敗します。 このようなプラグインには、スマート カードのドライバー、暗号化のプラグイン、パスワード フィルターなどがあります。

            (スマート カードのドライバー) などのドライバーである o LSA プラグインは、デジタル署名する必要があります。

            **注**  、 [Windows ハードウェア互換性プログラム](https://msdn.microsoft.com/library/windows/hardware/dn922588.aspx)Windows のドライバーがデジタル署名するための唯一の方法を提供します。 これについてはこの web サイトを参照する重要です。

             

    -   Microsoft Security Development Lifecycle (SDL) プロセス ガイダンスに準拠しています。

        -   すべてのプラグインがの該当する部分に準拠する必要も、 [Microsoft Security Development Lifecycle (SDL): プロセス ガイダンス](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)トピック。 たとえばを参照してください*いいえ共有セクション*付録 G の SDL のプロセスに記述されています。

        -   プラグインを適切なマイクロソフトの署名で署名が、場合でも、SDL のプロセスで非対応のプラグインの読み込みに失敗した可能性があります。

SDL の詳細については、次を参照してください[Microsoft Security Development Lifecycle (SDL): プロセス ガイダンス](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)。

開発者向けのガイドラインについては、次を参照してくださいおよび[開発者に関するガイドライン。](developer-guidelines.md)

## <a name="span-idtransactionmanagementspanspan-idtransactionmanagementspanspan-idtransactionmanagementspantransaction-management"></a><span id="Transaction_Management"></span><span id="transaction_management"></span><span id="TRANSACTION_MANAGEMENT"></span>トランザクションの管理


-   SCRM カードへのアクセスに使用する場合、トランザクションが、呼び出し元によって処理されますが、カード ミニドライバーに想定あります。
-   カードのミニドライバーを除くすべてのエントリを指していると想定できます[ **CardDeleteContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468715)カード トランザクションを保持しているによって呼び出されます。 これで想定できない**CardDeleteContext**カードが削除された可能性があるか、クリーンアップ プロシージャの一部として呼び出されたためです。
-   複数のコンテキストは、1 つのプロセスに存在できます。 呼び出す[ **CardDeleteContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468715) 1 つのプロセスにする必要がありますいない機能が妨げ、その他のコンテキスト。
-   カードの認証状態の処理が、カードのミニドライバーではない呼び出し元の責任もです。

## <a name="span-idconventionsspanspan-idconventionsspanspan-idconventionsspanconventions"></a><span id="Conventions"></span><span id="conventions"></span><span id="CONVENTIONS"></span>表記規則


### <a name="span-idstringsunicodeandansispanspan-idstringsunicodeandansispanspan-idstringsunicodeandansispanstrings-unicode-and-ansi"></a><span id="Strings__UNICODE_and_ANSI"></span><span id="strings__unicode_and_ansi"></span><span id="STRINGS__UNICODE_AND_ANSI"></span>文字列:UNICODE と ANSI

アプリケーション レベルでは、直接的または間接的に、ユーザー インターフェイスの要素として文字列が発生したは一般にします。 そのため、これらは、通常ローカライズする必要が (ユーザーの言語に翻訳) が認識できるようにします。 このため、ほとんどのアプリケーションを使用する文字列型です (つまり、UNICODE) の 2 バイト文字セットの種類に対応するために

ただし、スマート カードは、最小限のリソースで、ディレクトリ、ファイル、ユーザー、および具合を名前での非常にいくつかのオプションを使用して動作します。 文字列の文字セットは、1 バイトの ANSI は、文字列データのよりコンパクトな表現を提供します。

したがって、1 バイトの ANSI を予定している文字列バッファーとカードのミニドライバーの間、カード ミニドライバーの外部と必要な場合は、この文字型からの変換を実行する必要があります。

### <a name="span-iderrorhandlingspanspan-iderrorhandlingspanspan-iderrorhandlingspan-error-handling"></a><span id="_Error_Handling"></span><span id="_error_handling"></span><span id="_ERROR_HANDLING"></span> エラー処理

一貫性のあるエラーの処理、エラー、およびカードのミニドライバーの一貫した動作への応答を確実に、次の規則を従う必要があります。

-   NULL と無効なフラグを含む、無効なパラメーターをすべて返す s カード\_E\_無効な\_パラメーター。
-   正しくない PIN または間違ったキーでの試行をすべて返す s カード\_W\_間違った\_CHV します。
-   一般的なエラーが発生した場合、Api は s カードを返す\_E\_予期しません。

さらに、次のセクションで説明されている関数から返されるエラーは、s カードからする必要があります\_\*カテゴリ (*winerror.h*)。 S カードを使用すること勧めなど\_E\_無効な\_パラメーター (0x80100004) エラーではなく\_無効な\_パラメーター (0x00000057)。

**注**  ファイルは、I/O エラーのためのカードから読み取ることができませんまたはその他のいくつかの回復不能なデータを発行する場合に関連しない、カード上のファイルの実際の存在 s カードを返す、マイクロソフトの推奨通り\_E\_COMM\_データ\_LOST します。

S カードを返す\_E\_ファイル\_いない\_が見つかったは、このような状況では、包括的なエラー コードは、デバッグ情報を誤解を招くようです。

 

## <a name="span-idauthenticationandauthorizationspanspan-idauthenticationandauthorizationspanspan-idauthenticationandauthorizationspanauthentication-and-authorization"></a><span id="Authentication_and_Authorization"></span><span id="authentication_and_authorization"></span><span id="AUTHENTICATION_AND_AUTHORIZATION"></span>認証と承認


バージョン 6 以降、ミニドライバー インターフェイスは、従来の英数字文字列だけを超えるにピン留めの概念を拡張します。 詳細については、次を参照してください。"シークレット\_型 (列挙)"この仕様で後述します。

## <a name="span-idhandlingmemoryallocationsspanspan-idhandlingmemoryallocationsspanspan-idhandlingmemoryallocationsspanhandling-memory-allocations"></a><span id="Handling_Memory_Allocations"></span><span id="handling_memory_allocations"></span><span id="HANDLING_MEMORY_ALLOCATIONS"></span>メモリ割り当ての処理


この仕様で内部的にメモリ バッファーを割り当てることがすべての API 要素は呼び出すことによって[ **PFN\_CSP\_アロケーション**](https://msdn.microsoft.com/library/windows/hardware/dn468763)します。 このため、このようなすべてのメモリ バッファーを呼び出すことによって解放する必要があります[ **PFN\_CSP\_FREE**](https://msdn.microsoft.com/library/windows/hardware/dn468767)します。

使用して、カードのミニドライバーを実行するメモリの割り当てを行う必要があります[ **PFN\_CSP\_アロケーション**](https://msdn.microsoft.com/library/windows/hardware/dn468763)または[ **PFN\_CSP\_REALLOC**](https://msdn.microsoft.com/library/windows/hardware/dn468770)します。

## <a name="span-idcachingspanspan-idcachingspanspan-idcachingspancaching"></a><span id="Caching"></span><span id="caching"></span><span id="CACHING"></span>キャッシュ


Base CSP または KSP でカード インターフェイス レイヤーに書き込まれたまたは、スマート カードから読み取る必要があるデータの量を最小限に抑えるのデータ キャッシュを実装します。 データ キャッシュも利用可能になっての関数ポインターからを使用するカードのミニドライバーの[**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)構造、およびカードのミニドライバーは、強化するためにこれらのポインターを使用する必要がありますそのカードに格納されている内部データ ファイルをキャッシュすることによってパフォーマンス。

データ キャッシュには、カードに鮮度カウンターのキャッシュを保持するカードへの書き込みアクセスが必要です。 データ キャッシュ、カードにデータを書き込むことは不可能である場合、ミニドライバーを制御できます。

データ キャッシュを制御する方法の詳細については、CP の定義を参照してください\_カード\_キャッシュ\_MODE プロパティ[ **CardGetProperty** ](https://msdn.microsoft.com/library/windows/hardware/dn468729)このトピックの。指定。

## <a name="span-idmandatoryversioncheckingspanspan-idmandatoryversioncheckingspanspan-idmandatoryversioncheckingspanmandatory-version-checking"></a><span id="Mandatory_Version_Checking"></span><span id="mandatory_version_checking"></span><span id="MANDATORY_VERSION_CHECKING"></span>必須のバージョン チェック


すべてのカードのミニドライバーは、バージョン チェックを実装する必要があります。 バージョン、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)構造体が呼び出し元がサポートするバージョンとカードのミニドライバーが実際にサポートされるバージョンとの間のネゴシエーション。

### <a name="span-idcarddataversionchecksspanspan-idcarddataversionchecksspanspan-idcarddataversionchecksspancarddata-version-checks"></a><span id="CARD_DATA_Version_Checks"></span><span id="card_data_version_checks"></span><span id="CARD_DATA_VERSION_CHECKS"></span>カード\_データ バージョンのチェック

カード ミニドライバーの context 構造体の最小バージョンとして最低限のバージョンを定義する (つまり、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)構造) はサポートされているし、のレベルとして、現在のバージョンを定義します。このカード ミニドライバーのように設計されましたし、アイテムをから正常に返された有効であることが保証するすべてのカード ミニドライバーのセットの構造体の[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)します。 現在のバージョンが最小バージョン以上にする必要があります、カード\_データ\_現在\_で定義されているバージョン、 *Cardmod.h*します。

呼び出し元のアプリケーションを呼び出すと[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)を読み込もうと目的のバージョンを指定します。 この要求のバージョンが設定されている、 **dwVersion**内のメンバー、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)構造体。

要求されたバージョンが、カードのミニドライバーがでサポートされる最小バージョンより小さい場合[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)リビジョンの不一致エラーを返す必要があります (次のサンプル コードを参照してください)。

カードのミニドライバーを設定する必要があります、要求されたバージョンが少なくとも最低限のバージョンよりも大きくの場合、 **dwVersion**メンバーをサポートしていることは、要求されたバージョン未満の最上位バージョンです。

次のサンプル コードは、バージョンをチェックするときに、予想されるカードのミニドライバーの動作を示します。 これはの本文であると見なされます、 **CardAcquireContext**関数。 *pCardData*へのポインター、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)構造体がこの呼び出しに渡されます。

```ManagedCPlusPlus
#define MINIMUM_VERSION_SUPPORTED (4)
#define CURRENT_VERSION_SUPPORTED (7)

    // The lowest supported version is 4.
    If (pCardData->dwVersion < MINIMUM_VERSION_SUPPORTED)
    {
        dwError = (DWORD) ERROR_REVISION_MISMATCH;
        goto Ret;
    }

    // Set the version to what we support, but don’t exceed the
    // requested version
    pCardData->dwVersion =
       min(pCardData->dwVersion, CURRENT_VERSION_SUPPORTED);
```

**注**  カード ミニドライバーが返すバージョンは、呼び出し元のアプリケーションの目的に適していますが場合、これを適切に処理するために呼び出し元アプリケーションの責任は。

 

後**dwVersion**への呼び出しで設定されている[ **CardAcquireContext**](https://msdn.microsoft.com/library/windows/hardware/dn468701)、するには変更されません、呼び出し元またはカード ミニドライバーのいずれかによって、同じコンテキストになっている前提としています.

### <a name="span-idotherstructureversionchecksspanspan-idotherstructureversionchecksspanspan-idotherstructureversionchecksspanother-structure-version-checks"></a><span id="Other_Structure_Version_Checks"></span><span id="other_structure_version_checks"></span><span id="OTHER_STRUCTURE_VERSION_CHECKS"></span>その他の構造のバージョン チェック

その他のバージョン管理された構造とその他のカードのミニドライバー API メソッドは、バージョン管理は、場合と同じ、 [**カード\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn468748)構造は、1 つの例外。 格納する構造体で、API メソッドが呼び出された、 **dwVersion**を 0 に設定されているメンバーの場合は、このとして処理する必要を**dwVersion** 1 の値。

[ **CardRSADecrypt** ](https://msdn.microsoft.com/library/windows/hardware/dn468737)と[ **CardSignData** ](https://msdn.microsoft.com/library/windows/hardware/dn468741)関数はデータ構造のバージョン番号の特別な処理があります。渡されます。

 

 





