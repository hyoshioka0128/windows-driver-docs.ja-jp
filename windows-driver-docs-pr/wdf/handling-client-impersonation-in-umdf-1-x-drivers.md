---
title: UMDF 1.x ドライバーでクライアントの偽装を処理します。
description: UMDF 1.x ドライバーでクライアントの偽装を処理します。
ms.assetid: 25beab8c-e6b8-479b-ad60-fcc3b5b56a6d
keywords:
- ユーザー モード ドライバー フレームワーク WDK、権限借用
- UMDF WDK、権限借用
- ユーザー モード ドライバー WDK UMDF、権限借用
- 権限借用 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 329f57369e88186a9dcc750ed11fac48b4003a98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557536"
---
# <a name="handling-client-impersonation-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでクライアントの偽装を処理します。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーは通常、LocalService アカウントで実行し、ファイルまたは保護されたファイルなど、ユーザーの資格情報を必要とするリソースまたはその他の保護されたリソースにアクセスできません。 UMDF ドライバーは、通常、コマンドと、クライアント アプリケーションとデバイス間を流れるデータに対して動作します。 そのため、ほとんどの UMDF ドライバーでは、保護されたリソースはアクセスしません。

ただし、一部のドライバーでは、保護されたリソースへのアクセスを必要があります。 たとえば、UMDF ドライバーでは、クライアント アプリケーションが提供するファイルからのデバイスにファームウェアを読み込む可能性があります。 ファイルは、未承認のユーザー ファイルとデバイスの管理の変更できないようにするアクセス制御リスト (ACL) である可能性があります。 残念ながら、この ACL は、ファイルへのアクセス UMDF ドライバーも防止します。

フレームワークは、ドライバーのドライバーのクライアントを偽装し、保護されたリソースへのクライアントのアクセス権の取得を許可する権限の借用機能を提供します。

### <a name="enabling-impersonation"></a>権限借用を有効にします。

UMDF ドライバーのインストール パッケージと、クライアント アプリケーションの両方必要がありますを有効にするフレームワークの権限の借用機能では、次のように。

-   UMDF ドライバーのインストール パッケージの INF ファイルを含める必要があります、 **UmdfImpersonationLevel**ディレクティブと許容される最大の偽装レベルを設定します。 偽装を有効にすると、INF ファイルが含まれる場合にのみ、 **UmdfImpersonationLevel**ディレクティブ。 権限借用レベルを設定する方法についての詳細については、[INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)を参照してください。

-   クライアント アプリケーションでは、各ファイル ハンドル用に許可される偽装レベルを設定する必要があります。 アプリケーションでは、Microsoft Win32 の品質 (QoS) のサービスの設定の**CreateFile**許可される偽装レベルを設定します。 これらの設定の詳細については、次を参照してください。、 *dwFlagsAndAttributes*パラメーターの**CreateFile** Windows SDK のドキュメント。

### <a name="handling-impersonation-for-an-io-request"></a>I/O 要求の処理権限の借用

UMDF ドライバー、フレームワークは、次の順序で、I/O 要求の権限借用を処理します。

1.  ドライバーの呼び出し、 [ **IWDFIoRequest::Impersonate** ](https://msdn.microsoft.com/library/windows/hardware/ff559136)必要な偽装レベルを指定するメソッドと[ **IImpersonateCallback::OnImpersonate**](https://msdn.microsoft.com/library/windows/hardware/ff554916)コールバック関数。

2.  フレームワークは、要求された偽装レベルを確認します。 要求されたレベルが UMDF ドライバーのインストール パッケージと、クライアント アプリケーションを使用するレベルよりも大きい場合は、権限借用の要求は失敗します。 それ以外の場合、フレームワークは、クライアントを偽装し、すぐに呼び出し、 **OnImpersonate**コールバック関数。

**OnImpersonate**コールバック関数は、保護されたファイルを開くなど、要求された偽装レベルを必要とする操作のみを実行する必要があります。

UMDF にドライバーを許可しない**OnImpersonate** framework のオブジェクトのメソッドの呼び出しにコールバック関数。 これにより、ドライバーが偽装レベルを他のドライバーのコールバック機能またはその他のドライバーを公開しません。

**注**  バージョン 1.0 ~ UMDF の 1.7 で[ **IWDFIoRequest::Impersonate** ](https://msdn.microsoft.com/library/windows/hardware/ff559136)こと、クライアント アプリケーションと INF ファイルには、さらに、最高の権限借用レベルを付与場合は、ドライバーが要求される偽装レベルは低くなります。 UMFD バージョン 1.9 以降で、 **Impersonate**メソッドは、ドライバーが要求を権限借用レベルのみに付与します。

 

### <a name="passing-credentials-down-the-driver-stack"></a>下位のドライバー スタックの資格情報を渡す

ドライバーが受信すると、 [ **WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff561467)-型指定された I/O 要求、ドライバーは、カーネル モード ドライバーをドライバー スタックを I/O 要求を転送場合があります。 カーネル モード ドライバーには、権限の借用機能がないを**IWDFIoRequest::Impersonate** UMDF ベースのドライバーを提供します。

そのため、カーネル モード ドライバーがクライアントのユーザーの資格情報を受信するようにする場合 (の資格情報ではなく、[ドライバー ホスト プロセス](umdf-driver-host-process.md))、ドライバーを設定する必要があります、 [ **WDF\_要求\_送信\_オプション\_IMPERSONATE\_クライアント**](https://msdn.microsoft.com/library/windows/hardware/ff561462)フラグを呼び出すときに[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)を送信する、I/O ターゲットへの要求を作成します。 **送信**エラー メソッドを返しますのコード権限借用に失敗した場合、ドライバーによっても設定しない限り、 **WDF\_要求\_送信\_オプション\_権限借用\_無視\_エラー**フラグ。

ドライバーを呼び出す必要はありません**IWDFIoRequest::Impersonate** I/O ターゲットに、要求を送信する前にします。

要求を転送する下位レベルのドライバーも、クライアントの偽装レベルはドライバー スタックを下へ移動します。

### <a name="reducing-security-threats"></a>セキュリティの脅威を軽減

「特権が昇格される」攻撃の可能性を減らすためには、次の操作を行う必要があります。

-   権限借用の使用を回避しようとしてください。

    たとえば、ドライバーを使用する必要がありますファイルを開く権限借用の使用を避けるためには、クライアント アプリケーションできますファイルを開き I/O 操作を使用して、ドライバー ファイルの内容を送信します。

-   ドライバーが必要な最小の偽装レベルを使用します。

    できるだけ低く、ドライバーの INF ファイルでの偽装レベルを設定します。 ドライバーに権限借用を必要としない場合は含まれません、 **UmdfImpersonationLevel** INF ファイルでディレクティブ。

-   攻撃者は、ドライバーを悪用する機会を最小限に抑えます。

    **OnImpersonate**コールバック関数は、権限借用を必要とする操作のみを実行するコードの小さなセクションを含める必要があります。 たとえば、ファイル ハンドルを開くときにのみ、ドライバーが保護されたファイルにアクセスする場合権限借用が必要があります。 読み取りまたはファイルへの書き込み権限の借用は必要ありません。

 

 





