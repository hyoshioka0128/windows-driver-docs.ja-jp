---
title: UMDF 1.x ドライバーでのクライアント偽装の処理
description: UMDF 1.x ドライバーでのクライアント偽装の処理
ms.assetid: 25beab8c-e6b8-479b-ad60-fcc3b5b56a6d
keywords:
- ユーザーモードドライバーフレームワーク WDK、偽装
- UMDF WDK、偽装
- ユーザーモードドライバー WDK UMDF、偽装
- 権限借用 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fc53b3d055f7efc784be844f94513821b6becad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843639"
---
# <a name="handling-client-impersonation-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのクライアント偽装の処理


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーは通常、LocalService アカウントで実行され、保護されたファイルやその他の保護されたリソースなどのユーザー資格情報を必要とするファイルまたはリソースにはアクセスできません。 通常、UMDF ドライバーは、クライアントアプリケーションとデバイスとの間でやり取りされるコマンドとデータを操作します。 そのため、ほとんどの UMDF ドライバーは保護されたリソースにアクセスしません。

ただし、一部のドライバーでは、保護されたリソースへのアクセスが必要になる場合があります。 たとえば、UMDF ドライバーは、クライアントアプリケーションによって提供されるファイルからデバイスにファームウェアを読み込む場合があります。 このファイルには、承認されていないユーザーがファイルを変更してデバイスを制御することを防止するアクセス制御リスト (ACL) が含まれている場合があります。 残念ながら、この ACL は、UMDF ドライバーがファイルにアクセスできないようにします。

フレームワークには、ドライバーがドライバーのクライアントを偽装し、保護されたリソースへのクライアントのアクセス権を取得できるようにする偽装機能が用意されています。

### <a name="enabling-impersonation"></a>偽装の有効化

次のように、UMDF ドライバーのインストールパッケージとクライアントアプリケーションの両方で、フレームワークの偽装機能を有効にする必要があります。

-   UMDF ドライバーのインストールパッケージの INF ファイルには、 **UmdfImpersonationLevel**ディレクティブを含め、許容される最大の偽装レベルを設定する必要があります。 権限借用は、INF ファイルに**UmdfImpersonationLevel**ディレクティブが含まれている場合にのみ有効になります。 偽装レベルの設定の詳細については、「 [INF ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。

-   クライアントアプリケーションは、各ファイルハンドルに対して許可されている偽装レベルを設定する必要があります。 アプリケーションでは、Microsoft Win32 **CreateFile**関数のサービス品質 (QoS) 設定を使用して、許可される偽装レベルを設定します。 これらの設定の詳細については、Windows SDK のドキュメントの**CreateFile**の*dwFlagsAndAttributes*パラメーターを参照してください。

### <a name="handling-impersonation-for-an-io-request"></a>I/o 要求の偽装の処理

UMDF ドライバーとフレームワークは、次の順序で i/o 要求の偽装を処理します。

1.  ドライバーは[**IWDFIoRequest:: Impersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-impersonate)メソッドを呼び出して、必要な偽装レベルと[**IImpersonateCallback:: onimpersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iimpersonatecallback-onimpersonate)コールバック関数を指定します。

2.  フレームワークは、要求された偽装レベルを確認します。 要求されたレベルが、UMDF ドライバーのインストールパッケージおよびクライアントアプリケーションが許可するレベルよりも大きい場合、権限借用要求は失敗します。 それ以外の場合、フレームワークはクライアントの権限を借用し、すぐに**Onimpersonate**コールバック関数を呼び出します。

**Onimpersonate**コールバック関数は、保護されたファイルを開くなど、要求された偽装レベルを必要とする操作のみを実行する必要があります。

UMDF では、ドライバーの**Onimpersonate**コールバック関数がフレームワークのオブジェクトメソッドを呼び出すことはできません。 これにより、ドライバーが偽装レベルを他のドライバーコールバック関数やその他のドライバーに公開しないようにすることができます。

**注**   UMDF のバージョン 1.0 ~ 1.7 では、 [**IWDFIoRequest:: Impersonate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-impersonate)は、ドライバーが要求する偽装レベルが低い場合でも、クライアントアプリケーションと INF ファイルで許可される最も高い偽装レベルを付与します。 UMFD バージョン1.9 以降では、 **Impersonate**メソッドによって、ドライバーが要求する偽装レベルだけが付与されます。

 

### <a name="passing-credentials-down-the-driver-stack"></a>資格情報をドライバースタックに渡す

ドライバーが[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_request_type)によって型指定された i/o 要求を受信すると、ドライバーが i/o 要求をドライバースタックからカーネルモードドライバーに転送する場合があります。 カーネルモードドライバーには、 **IWDFIoRequest:: Impersonate**が UMDF ベースのドライバーに提供する偽装機能がありません。

したがって、カーネルモードドライバーがクライアントのユーザー資格情報 ([ドライバーホストプロセス](umdf-driver-host-process.md)の資格情報) を受信するようにするには、ドライバーで[**WDF\_REQUEST\_SEND\_オプションを IMPERSONATE\_IMPERSONATE に設定する必要があり\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_request_send_options_flags)フラグ。 [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)を呼び出して、作成要求を i/o ターゲットに送信します。 この**メソッドで**は、偽装の試行が失敗した場合に、エラーコードが返されます。ただし、ドライバーが WDF\_\_要求を設定している場合は、 **\_オプション\_偽装\_無視\_エラー**フラグが無視されます。

ドライバーは、要求を i/o ターゲットに送信する前に**IWDFIoRequest:: Impersonate**を呼び出す必要はありません。

下位レベルのドライバーも要求を転送する場合、クライアントの偽装レベルはドライバースタックを経由します。

### <a name="reducing-security-threats"></a>セキュリティの脅威の軽減

"特権の昇格" 攻撃の可能性を低減するには、次のことを行う必要があります。

-   偽装を使用しないようにしてください。

    たとえば、偽装を使用してドライバーが使用する必要のあるファイルを開くことを避けるために、クライアントアプリケーションはファイルを開き、i/o 操作を使用してファイルの内容をドライバーに送信することができます。

-   ドライバーに必要な最も低い偽装レベルを使用します。

    ドライバーの INF ファイルの偽装レベルをできるだけ低く設定します。 ドライバーが偽装を必要としない場合は、 **UmdfImpersonationLevel**ディレクティブを INF ファイルに含めないでください。

-   攻撃者がドライバーを悪用する機会を最小限に抑えます。

    **Onimpersonate**コールバック関数には、偽装を必要とする操作のみを実行するコードの小さなセクションを含める必要があります。 たとえば、保護されたファイルにアクセスするドライバーは、ファイルハンドルを開いたときにのみ偽装を必要とします。 ファイルに対して読み取りまたは書き込みを行うための権限借用は必要ありません。

 

 





