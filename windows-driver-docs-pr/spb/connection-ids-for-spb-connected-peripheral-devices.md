---
title: SPB 接続周辺機器の接続 ID
description: ドライバーが単純な周辺機器バス (sp B) 上の周辺機器に I/O 要求を送信する前に、ドライバーは、デバイスへの論理接続を開く必要があります。
ms.assetid: 234B5858-5930-40AD-BE4C-4A774A809D10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9b66cbbb6cab93960503be1e800503c2a4810cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348072"
---
# <a name="connection-ids-for-spb-connected-peripheral-devices"></a>SPB 接続周辺機器の接続 ID


ドライバーは、周辺機器の I/O 要求送信する前に、[シンプルな周辺機器のバス](https://msdn.microsoft.com/library/windows/hardware/hh450903)(SPB) ドライバーは、デバイスへの論理接続を開く必要があります。 この接続を介して、ドライバーは、送信、読み取りと書き込みをして、デバイスからデータを転送する要求。 さらに、ドライバー、I/O コントロール (IOCTL) 要求を送信できます SPB 固有の操作を実行するデバイス。




システムの起動時には、プラグ アンド プレイ (PnP) マネージャーは、PnP デバイスと非 PnP デバイスの両方を列挙します。 非 PnP の周辺機器、SPB に固定接続があるは、PnP マネージャーは、デバイスにアクセスする方法を説明する接続パラメーターのセットを取得する、ハードウェア プラットフォームの ACPI のファームウェアを照会します。 これらの接続パラメーターは、バスをデバイスが接続されているし、バスのアドレスとバスのクロック周波数デバイスと通信するために、コント ローラーを必要とするなどの他の情報を含める SPB コント ローラーを識別します。

PnP マネージャー id を割り当てます: と呼ばれる、*接続 ID*-SPB に接続されている周辺機器の接続パラメーターにします。 PnP マネージャーは、この ID と呼ばれるシステム データ ストア内での接続パラメーターを格納、*リソース ハブ*します。 (リソース ハブは PnP マネージャーが SPB に接続されている周辺機器に関する構成情報を格納する内部のデータストアです)。接続 ID は、ドライバーは、それらを明示的に指定する必要があるように、これらのパラメーターをカプセル化します。

Sp B に接続されている周辺機器デバイスのドライバーでは、ドライバーの割り当てられたハードウェア リソースの一部として、デバイスの接続 ID を受け取ります。 周辺機器のデバイスのドライバーが、デバイスへの接続を開くシステム関数を呼び出すと、ドライバーは、関数を使用してリソース ハブからデバイスの接続パラメーターを取得する接続 ID を提供します。

ドライバーの開発者は、いずれかを使用できます、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff560442)(UMDF) または[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)SPB に接続されている周辺機器デバイスのドライバーをビルドするには、(KMDF)。 UMDF ドライバー (を接続 ID を含む) のリソースを受信するときに、フレームワークが、ドライバーの[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)メソッド。 KMDF ドライバーの受信中に、ハードウェア リソースを[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック。

そのリソースの一覧で接続 Id を受信する周辺 UMDF ドライバーを有効にするドライバーをインストールする INF ファイルは、WDF 固有で、次のディレクティブを含める必要があります**DDInstall**セクション。

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**このディレクティブの詳細については、次を参照してください。 [INF ファイルで WDF ディレクティブを指定する](https://msdn.microsoft.com/library/windows/hardware/ff560526)します。 このディレクティブを使用する (対応する INF ファイルをビルドするために使用) INX ファイルの例は、次を参照してください。、 [SpbAccelerometer](https://go.microsoft.com/fwlink/p/?LinkId=618052)ドライバー サンプル。

ドライバーをリソースとして受信する接続 ID は、64 ビットの整数ですが、ドライバーを使用して、この ID をリソース ハブからの接続パラメーターを取得するために使用するデバイスのパス名に組み込む必要があります。 デバイス パス名は、ドライバーの呼び出しを作成する、**リソース\_ハブ\_作成\_パス\_FROM\_ID** Reshub.h ヘッダー ファイルで宣言されている関数。

UMDF ドライバーが呼び出し SPB に接続されている周辺機器への論理接続を開くには、するには、 [ **IWDFRemoteTarget::OpenFileByName** ](https://msdn.microsoft.com/library/windows/hardware/ff560273)メソッドをおよび KMDF ドライバーを呼び出す、 [ **WdfIoTargetOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff548634)メソッド。 いずれかの方法では、入力パラメーターとして、デバイス パス名が必要です。

接続 Id を使用して、sp B に接続されている周辺機器への論理接続を開く UMDF および KMDF のコード例を次のトピックを参照してください。

[ユーザー モード SPB の周辺機器のドライバーのハードウェア リソース](https://msdn.microsoft.com/library/windows/hardware/hh450837)
[カーネル モード SPB の周辺機器のドライバーのハードウェア リソース](https://msdn.microsoft.com/library/windows/hardware/hh698217)ユーザー モード アプリケーションが SPB 接続への論理接続を開くことができません周辺機器とこれらのデバイスに直接 I/O 要求を送信することはできません。

1 つだけのドライバーでは、一度に SPB に接続されている周辺機器への開いた論理接続を保持できます。 別のドライバーによって、同じデバイスに 2 番目の接続を開こうとして失敗します。

 

 




