---
title: Acl とデバイス スタック
description: Acl とデバイス スタック
ms.assetid: DAFC851D-E808-4588-86D2-E608584FD05B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd6567b89243c3f685217e250e0a7678c89110cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559377"
---
# <a name="acls-and-the-device-stack"></a>Acl とデバイス スタック


ボリュームとデバイスへのアクセスは、それぞれのインターフェイスのそれぞれに設定されている Acl によって制御されます。 デバイス インターフェイスの Acl を確認します。

-   かどうかをデバイスを識別するハンドルを開くアプリケーションを要求すると、ユーザーは、要求されたアクセス許可を受け取ります。

-   コマンドは、デバイスに送信できます。

CD ドライブなどのリムーバブル メディアのドライバー スタックは、1 つ以上のインターフェイスを持つことができます。

-   ポート ドライバーによって管理されると、PDO に関連付けられている 1 つ。

-   クラスのドライバー (Cdrom.sys) によって管理されると、FDO に関連付けられている 1 つ。

UFD などのホット プラグ可能なデバイスのドライバー スタックは、ボリューム マネージャーにもインターフェイスを提供します。 たとえば、書式設定ユーティリティでは、ボリュームをフォーマットするボリュームのインターフェイスを識別するハンドルを開くは。

直接アクセスは、アプリケーションは、ドライブを識別するハンドルを開くポート ドライバーとドライバー インターフェイスのクラスを使用できます。 たとえば、アプリケーションは、物理ドライブ インターフェイスを介してデバイスに SCSI コマンドを送信する場合、プロセスはとおりです。

-   まず、アプリケーションは、読み取り/書き込みアクセスのドライブ インターフェイスを識別するハンドルを開きます。

-   ハンドルが正常に開かれた後、アプリケーションが使用できる、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) SCSI 要求をデバイスに送信する関数。

ドライバー スタックは、デバイスのインターフェイスを作成するとき、ACL は、そのデバイスに適用されます。 ACL のアクセス制御要素 (ACE) では、ユーザー グループを説明し、アクセス許可に関連します。 など、Administrators グループの ACE は管理者がそのデバイス インターフェイスのある読み取り/書き込みアクセスのアクセス許可を記述する場合もあります。

アプリケーションがデバイスを識別するハンドルを開くしようとすると、I/O マネージャーは、呼び出し元が要求されたアクセスを許可されているかどうかを判断するのにデバイスの ACL を使用します。 たとえば、呼び出し元は、読み取り/書き込みアクセスのデバイスを識別するハンドルを要求している場合は、ハンドルを読み取って、そのインターフェイスを使用して書き込み、呼び出し元が許可されている場合にのみ提供されます。 呼び出し元が要求されたアクセス許可を持たない場合は、I/O マネージャー アクセスが拒否エラーが返され、ハンドルが開いている要求が失敗しました。

デバイスの Acl は、これらの Windows コンポーネントによって作成されます。I/O マネージャー、PnP マネージャー、およびリムーバブル記憶装置の新しいグループ ポリシー サービス。

## <a name="span-idiomanagerandremovablemediadeviceaclsspanspan-idiomanagerandremovablemediadeviceaclsspanspan-idiomanagerandremovablemediadeviceaclsspanio-manager-and-removable-media-device-acls"></a><span id="I_O_Manager_and_Removable_Media_Device_ACLs"></span><span id="i_o_manager_and_removable_media_device_acls"></span><span id="I_O_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>I/O マネージャーとリムーバブル メディア デバイスの Acl


ドライバー スタックは、デバイス オブジェクトを作成するとき、I/O マネージャーは、既定のデバイスの種類に基づいている ACL を設定します。 既定の ACL へのフル アクセスを提供するシステムと、管理者には実行のみその他のユーザーへのアクセス。

-   デバイス オブジェクトとそれらの CD ドライブなどのリムーバブル メディア デバイスのディスク ファイルを定義しているデバイス オブジェクトの既定では、I/O マネージャーが %1!IU! グループのフル アクセスを許可\_リムーバブル\_メディア特性。

    **注**  Windows Vista では、前に %1!IU! のエントリが I/O マネージャーによって設定された ACL に存在しません。 完全な Windows Vista を以降では I/O マネージャー、IU グループへのアクセスをアプリケーションは、既に説明したように、特権の昇格を必要とせずのボリュームに直接アクセスを受信できるようにします。 ただし、UFD デバイスを設定しないでください、**リムーバブル**I/O マネージャーはそのとして扱いませんリムーバブルため、これから、プロパティは利用できません。

     

-   ディスクのクラス ドライバー ファイルを設定する\_リムーバブル記憶域\_メディア特性の id データ (SCSI 問い合わせコマンドへの応答内のデバイスからの受信) の場合、**リムーバブル記憶域**プロパティ セット。 UFD デバイスでは、本当にリムーバブル メディアでない場合でも、このプロパティが設定されているので、I/O マネージャーはリムーバブル ディスクとしてこのようなデバイスを処理し、%1!IU! のグループを読み取るし、ボリュームへの書き込みアクセスを提供します。

-   既定では、I/O マネージャーは、リモートで接続しているユーザーの実行のアクセスのみのリムーバブル メディア (CD デバイス) のデバイス オブジェクトとそれらのディスク デバイス オブジェクトのファイルがあるファイル\_リムーバブル\_メディアの特徴のセット。 リモート ユーザーが CD または DVD ドライブを使用してデータを書き込むことはできません、このためには、光学式メディアにバックアップを実行またはまたはリムーバブル ディスク フォーマット。 管理者は、既定の動作をオーバーライドするリムーバブル記憶域へのアクセス グループ ポリシーを設定できます。 このポリシーが設定されている場合は、書き込み機能もと I/O マネージャー許可完全は読み取りを許可するこれらのデバイス用のリモート ユーザーにアクセスします。

## <a name="span-idpnpmanagerandremovablemediadeviceaclsspanspan-idpnpmanagerandremovablemediadeviceaclsspanspan-idpnpmanagerandremovablemediadeviceaclsspanpnp-manager-and-removable-media-device-acls"></a><span id="PnP_Manager_and_Removable_Media_Device_ACLs"></span><span id="pnp_manager_and_removable_media_device_acls"></span><span id="PNP_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>PnP マネージャーとリムーバブル メディア デバイスの Acl


デバイスのドライバー スタックが開始されると、PnP マネージャーは、レジストリ内のデバイスのキーは、そのデバイスのセキュリティ記述子を指定する場合にのみ、デバイス上の ACL を変更します。 使用して、デバイスの製造元がこの記述子の設定**SetupDiSetDeviceRegistryProperty**プロパティが次のように設定します。

|          |                                  |
|----------|----------------------------------|
| プロパティ | SPDRP\_セキュリティ                  |
| Value    | **セキュリティ\_記述子**         |
| サイズ     | **sizeof**(セキュリティ\_記述子) |

 

これらのプロパティは、INF ファイルで、関連するパラメーターを指定することで、ドライバー パッケージ インストーラーからも設定できます。

## <a name="span-idgrouppolicyserviceforremovablestoragedevicesaclsspanspan-idgrouppolicyserviceforremovablestoragedevicesaclsspanspan-idgrouppolicyserviceforremovablestoragedevicesaclsspangroup-policy-service-for-removable-storage-devices-acls"></a><span id="Group_Policy_Service_for_Removable_Storage_Devices_ACLs"></span><span id="group_policy_service_for_removable_storage_devices_acls"></span><span id="GROUP_POLICY_SERVICE_FOR_REMOVABLE_STORAGE_DEVICES_ACLS"></span>リムーバブル記憶域デバイスの Acl のグループ ポリシー サービス


これは、管理者が CD または DVD、テープおよびフロッピー ディスク ドライブ、およびグループ ポリシー フレームワークを通じて WPD デバイス用のディスク ボリュームのインターフェイスとボリューム インターフェイスの Acl を設定できるようにする Windows サービスです。 このグループ ポリシーを動的に変更することができます。 マシンにポリシーが適用されると、サービスは、デバイスの ACL を更新します。 このサービスによって適用される ACL では、既定の I/O マネージャーや PnP マネージャーによって設定された ACL をオーバーライドします。

グループ ポリシー サービスは、ディスクのクラス ドライバーが提供されるインターフェイスではなく、ディスクのボリュームのインターフェイスで ACL を設定します。 これは、I/O マネージャーが、呼び出し元が必要なアクセス許可を持つかどうかを判断するの対応するボリューム オブジェクトの ACL を使用してアプリケーションをアクセスすると、ボリュームのファイルとディレクトリ、ためにです。 そのため、ボリューム デバイス オブジェクトの ACL を設定することにより、グループ ポリシー サービスでは、そのボリュームの管理者が設定したアクセス権に適用されます。

## <a name="span-idsecuritycheckprocessspanspan-idsecuritycheckprocessspanspan-idsecuritycheckprocessspansecurity-check-process"></a><span id="Security_Check_Process"></span><span id="security_check_process"></span><span id="SECURITY_CHECK_PROCESS"></span>セキュリティ確認の処理


アプリケーションはしようとすると、デバイス インターフェイスへのハンドルを開くと、I/O マネージャーがで要求されているアクセス権限がユーザーに許可されているかどうかを確認します、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)呼び出します。 ハンドルが開かれた場合は、それ以外の場合、呼び出しはエラーへのアクセス失敗\_が拒否されました。

ハンドルが開かれた後、アプリケーション コマンドを送信できる、デバイスに直接通常 IOCTL を使用しています。 たとえば、SCSI パススルー コマンドを送信するアプリケーションは使用**IOCTL\_SCSI\_渡す\_を通じて**または**IOCTL\_SCSI\_のパス\_を通じて\_直接**します。

-   **IOCTL\_ディスク\_取得\_パーティション\_情報**読み取りアクセスだけが必要です。

-   **IOCTL\_SCSI\_渡す\_を通じて**と**IOCTL\_SCSI\_渡す\_を通じて\_直接**に呼び出し元が必要です読み取り/書き込みアクセスの両方のインターフェイス (これは、記憶装置デバイス ドライバーによって提供されます) を識別するハンドルを開きました。

SCSI パススルー要求で指定されたコマンド記述子ブロック (CDB) オペコードは、読み取り、書き込み、両方の読み取りおよび書き込みアクセス権が必要であるかどうかを判断するのにはチェックされません。 Windows が常に、アプリケーションだけを行う、読み取り、書き込み、またはデータが転送されずに場合でもにパススルーの要求の読み取りと書き込み用に開かれるデバイスを識別するハンドルが必要です。

**IOCTL\_ディスク\_を確認してください**で要求されたアクセス許可に関係なく送信できる、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)呼び出します。 その IOCTL に必要なアクセス許可をチェックし、比較することで呼び出し元に付与されるアクセス許可と I/O マネージャー受け取ると、IOCTL、 **CreateFile**呼び出します。 IOCTL がターゲット デバイスに送信される一致がある場合IOCTL 呼び出しをアクセス エラーで失敗するそれ以外の場合、\_が拒否されました。

たとえば、次のように、呼び出し元には、次のように、読み取り専用アクセスのハンドルが開かれている場合です。

-   **IOCTL\_SCSI\_渡す\_を通じて**アクセス エラーで失敗\_読み取りおよび書き込みアクセスを必要とするために拒否されました。

-   **IOCTL\_ディスク\_取得\_パーティション\_情報**読み取り専用のアクセスを必要とするために、ドライバー スタックに送信されます。

 

 




