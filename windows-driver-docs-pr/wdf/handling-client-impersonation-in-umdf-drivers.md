---
title: UMDF ドライバーでのクライアント偽装の処理
description: このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) ドライバー以降 UMDF バージョン 2 では、保護されたリソースにアクセスする方法について説明します。
ms.assetid: 02EA93CE-3C4D-4F6F-8E58-DD78EBDB19DE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 134b32c1987b50e7cacbdec8e1aa2df10ecf3e5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382857"
---
# <a name="handling-client-impersonation-in-umdf-drivers"></a>UMDF ドライバーでのクライアント偽装の処理


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) ドライバー以降 UMDF バージョン 2 では、保護されたリソースにアクセスする方法について説明します。

UMDF ドライバーは通常、LocalService アカウントで実行し、ファイルまたは保護されたファイルなど、ユーザーの資格情報を必要とするリソースまたはその他の保護されたリソースにアクセスできません。 UMDF ドライバーは、通常、コマンドと、クライアント アプリケーションとデバイス間を流れるデータに対して動作します。 そのため、ほとんどの UMDF ドライバーでは、保護されたリソースはアクセスしません。

ただし、一部のドライバーでは、保護されたリソースへのアクセスを必要があります。 たとえば、UMDF ドライバーでは、クライアント アプリケーションが提供するファイルからのデバイスにファームウェアを読み込む可能性があります。 ファイルは、未承認のユーザー ファイルとデバイスの管理の変更できないようにするアクセス制御リスト (ACL) である可能性があります。 残念ながら、この ACL は、ファイルへのアクセス UMDF ドライバーも防止します。

フレームワークは、ドライバーのドライバーのクライアントを偽装し、保護されたリソースへのクライアントのアクセス権の取得を許可する権限の借用機能を提供します。

### <a name="enabling-impersonation"></a>権限借用を有効にします。

UMDF ドライバーのインストール パッケージと、クライアント アプリケーションの両方必要がありますを有効にするフレームワークの権限の借用機能では、次のように。

-   UMDF ドライバーのインストール パッケージの INF ファイルを含める必要があります、 **UmdfImpersonationLevel**ディレクティブと許容される最大の偽装レベルを設定します。 偽装を有効にすると、INF ファイルが含まれる場合にのみ、 **UmdfImpersonationLevel**ディレクティブ。 権限借用レベルを設定する方法についての詳細については、次を参照してください。 [INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)します。

-   クライアント アプリケーションでは、各ファイル ハンドル用に許可される偽装レベルを設定する必要があります。 アプリケーションでは、Microsoft Win32 の品質 (QoS) のサービスの設定の**CreateFile**許可される偽装レベルを設定します。 これらの設定の詳細については、次を参照してください。、 *dwFlagsAndAttributes*パラメーターの**CreateFile** Windows SDK のドキュメント。

### <a name="handling-impersonation-for-an-io-request"></a>I/O 要求の処理権限の借用

UMDF ドライバー、フレームワークは、次の順序で、I/O 要求の権限借用を処理します。

1.  ドライバー呼び出し、 [ **WdfRequestImpersonate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)必要な偽装レベルを指定するメソッドをおよび[ *EvtRequestImpersonate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)コールバック関数。

2.  フレームワークは、要求された偽装レベルを確認します。 要求されたレベルが UMDF ドライバーのインストール パッケージと、クライアント アプリケーションを使用するレベルよりも大きい場合は、権限借用の要求は失敗します。 それ以外の場合、フレームワークは、クライアントを偽装し、すぐに呼び出し、 [ *EvtRequestImpersonate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)コールバック関数。

[ *EvtRequestImpersonate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)コールバック関数は、保護されたファイルを開くなど、要求された偽装レベルを必要とする操作のみを実行する必要があります。

フレームワークは、ドライバーを許可しない[ *EvtRequestImpersonate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate) framework のオブジェクトのメソッドの呼び出しにコールバック関数。 これにより、ドライバーが偽装レベルを他のドライバーのコールバック機能またはその他のドライバーを公開しません。

ベスト プラクティスとして、ドライバーはいけない[キャンセルできるように](canceling-i-o-requests.md)呼び出す前に、I/O 要求の[ **WdfRequestImpersonate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)要求に必要です。

[ **WdfRequestImpersonate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate)メソッドは、ドライバーが要求を権限借用レベルのみに付与します。

### <a name="passing-credentials-down-the-driver-stack"></a>下位のドライバー スタックの資格情報を渡す

ドライバーが受信すると、 [ **WdfRequestTypeCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ne-wdfrequest-_wdf_request_type)-型指定された I/O 要求、ドライバーは、カーネル モード ドライバーをドライバー スタックを I/O 要求を転送場合があります。 カーネル モード ドライバーには、権限の借用機能がないを[ **WdfRequestImpersonate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate) UMDF ドライバーを提供します。

そのため、カーネル モード ドライバーがクライアントのユーザーの資格情報を受信するようにする場合 (の資格情報ではなく、[ドライバー ホスト プロセス](umdf-driver-host-process.md))、ドライバーを設定する必要があります、 [ **WDF\_要求\_送信\_オプション\_IMPERSONATE\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)フラグを呼び出すときに[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)の作成を送信するにはI/O ターゲットへの要求します。 **送信**エラー メソッドを返しますのコード権限借用に失敗した場合、ドライバーによっても設定しない限り、 **WDF\_要求\_送信\_オプション\_権限借用\_無視\_エラー**フラグ。

次の例は、UMDF ドライバーを使用して方法、 **WDF\_要求\_送信\_オプション\_IMPERSONATE\_クライアント**フラグには、ファイルの作成要求を送信するには/O ターゲット。 ドライバーの INF ファイルに含める必要がありますも、 **UmdfImpersonationLevel**ディレクティブ上で説明したようにします。

```cpp
WDFIOTARGET iotarget;
WDF_REQUEST_SEND_OPTIONS options;
NTSTATUS status;
WDF_REQUEST_PARAMETERS params;
ULONG sendFlags;  
 
WDF_REQUEST_PARAMETERS_INIT(&params);
WdfRequestGetParameters(Request, &params);
   
sendFlags = WDF_REQUEST_SEND_OPTION_SYNCHRONOUS;
if (params.Type == WdfRequestTypeCreate) {
    sendFlags |= WDF_REQUEST_SEND_OPTION_IMPERSONATE_CLIENT;
}
   
WDF_REQUEST_SEND_OPTIONS_INIT(&options, sendFlags);
if (WdfRequestSend(Request,
                   iotarget,
                   &options
                   ) == FALSE) {
    status = WdfRequestGetStatus(Request);
}
```

ドライバーを呼び出す必要はありません[ **WdfRequestImpersonate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestimpersonate) I/O ターゲットに、要求を送信する前にします。

要求を転送する下位レベルのドライバーも、クライアントの偽装レベルはドライバー スタックを下へ移動します。

### <a name="reducing-security-threats"></a>セキュリティの脅威を軽減

「特権が昇格される」攻撃の可能性を減らすためには、次の操作を行う必要があります。

-   権限借用の使用を回避しようとしてください。

    たとえば、ドライバーを使用する必要がありますファイルを開く権限借用の使用を避けるためには、クライアント アプリケーションできますファイルを開き I/O 操作を使用して、ドライバー ファイルの内容を送信します。

-   ドライバーが必要な最小の偽装レベルを使用します。

    できるだけ低く、ドライバーの INF ファイルでの偽装レベルを設定します。 ドライバーに権限借用を必要としない場合は含まれません、 **UmdfImpersonationLevel** INF ファイルでディレクティブ。

-   攻撃者は、ドライバーを悪用する機会を最小限に抑えます。

    [ *EvtRequestImpersonate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_impersonate)コールバック関数は、権限借用を必要とする操作のみを実行するコードの小さなセクションを含める必要があります。 たとえば、ファイル ハンドルを開くときにのみ、ドライバーが保護されたファイルにアクセスする場合権限借用が必要があります。 読み取りまたはファイルへの書き込み権限の借用は必要ありません。

 

 





