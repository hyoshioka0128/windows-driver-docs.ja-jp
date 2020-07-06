---
title: ACL とデバイス スタック
description: ACL とデバイス スタック
ms.assetid: DAFC851D-E808-4588-86D2-E608584FD05B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c20f527b205391ffdb0878558c82681b911f4858
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968429"
---
# <a name="acls-and-the-device-stack"></a>ACL とデバイス スタック


ボリュームとデバイスへのアクセスは、それぞれのインターフェイスに設定されている Acl によって制御されます。 デバイスインターフェイスの Acl は、次のことを決定します。

-   アプリケーションがデバイスへのハンドルを開くように要求したときに、ユーザーが要求されたアクセス許可を受け取るかどうかを指定します。

-   どのコマンドをデバイスに送信できますか。

CD ドライブなどのリムーバブルメディアのドライバースタックには、複数のインターフェイスを含めることができます。

-   PDO に関連付けられているもの。これは、ポートドライバーによって管理されます。

-   FDO に関連付けられているもの。クラスドライバー (Cdrom.sys) によって管理されます。

UFD などのホットプラグ可能なデバイスのドライバースタックには、ボリュームマネージャーへのインターフェイスも用意されています。 たとえば、フォーマットユーティリティはボリュームインターフェイスへのハンドルを開き、ボリュームをフォーマットします。

直接アクセスの場合、アプリケーションはポートドライバーおよびクラスドライバーインターフェイスを使用して、ドライブへのハンドルを開くことができます。 たとえば、アプリケーションが物理ドライブインターフェイスを使用して SCSI コマンドをデバイスに送信する場合、プロセスは次のようになります。

-   アプリケーションでは、まず、読み取りおよび書き込みアクセスのためのドライブインターフェイスへのハンドルを開きます。

-   ハンドルが正常に開かれると、アプリケーションは[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を使用してデバイスに SCSI 要求を送信できます。

ドライバースタックによってデバイスインターフェイスが作成されると、そのデバイスに ACL が適用されます。 ACL のアクセス制御要素 (ACE) は、ユーザーグループおよび関連するアクセス許可を記述します。 たとえば、管理者グループの ACE は、そのデバイスインターフェイスに対して管理者が持っている読み取りと書き込みのアクセス許可を記述する場合があります。

アプリケーションがデバイスへのハンドルを開こうとすると、i/o マネージャーはデバイスの ACL を使用して、要求されたアクセスが呼び出し元に許可されているかどうかを判断します。 たとえば、呼び出し元がデバイスへのハンドルを読み取りおよび書き込みアクセス用に要求した場合、そのインターフェイスを使用して呼び出し元が読み取りと書き込みを許可されている場合にのみ、ハンドルが提供されます。 呼び出し元に要求されたアクセス許可がない場合、i/o マネージャーはアクセス拒否エラーを返し、open handle 要求は失敗します。

デバイス Acl は、次の Windows コンポーネント (i/o マネージャー、PnP マネージャー、リムーバブル記憶装置用の新しいグループポリシーサービス) によって作成されます。

## <a name="span-idi_o_manager_and_removable_media_device_aclsspanspan-idi_o_manager_and_removable_media_device_aclsspanspan-idi_o_manager_and_removable_media_device_aclsspanio-manager-and-removable-media-device-acls"></a><span id="I_O_Manager_and_Removable_Media_Device_ACLs"></span><span id="i_o_manager_and_removable_media_device_acls"></span><span id="I_O_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>I/o マネージャーとリムーバブルメディアデバイスの Acl


ドライバースタックがデバイスオブジェクトを作成すると、i/o マネージャーによって、デバイスの種類に基づく既定の ACL が設定されます。 既定の ACL では、システムと管理者へのフルアクセスが付与され、他のすべてのユーザーに対してのみ実行アクセスが許可されます。

-   既定では、i/o マネージャーによって、IU グループに、CD ドライブなどのリムーバブルメディアデバイスの場合はデバイスオブジェクトのフルアクセスが許可され、ファイルのリムーバブルメディア特性が定義されているディスクデバイスオブジェクトの場合はフルアクセスが付与され \_ \_ ます。

    **メモ**   Windows Vista より前の場合、IU のエントリは、i/o マネージャーによって設定された ACL には存在しませんでした。 Windows Vista 以降、i/o マネージャーは IU グループへのフルアクセスを提供しています。これにより、前に説明したように、アプリケーションは特権の昇格を必要とせずに、ボリュームへの直接アクセスを受け取ることができます。 ただし、**リムーバブル**プロパティが設定されていない UFD デバイスは、i/o マネージャーではリムーバブルとして扱われないため、これを利用することはできません。

     

-   ディスククラスドライバーは、 \_ \_ (SCSI 照会コマンドに応答してデバイスから受信された) id データが**リムーバブル**プロパティを設定している場合に、ファイルのリムーバブルメディア特性を設定します。 一部の UFD デバイスは、実際にはリムーバブルメディアではなくてもこのプロパティを設定するため、i/o マネージャーは、このようなデバイスをリムーバブルディスクとして扱い、IU グループにボリュームへの読み取りおよび書き込みアクセスを提供します。

-   既定では、i/o マネージャーは、リムーバブルメディアデバイスオブジェクト (CD デバイス) に対してリモート接続されているユーザーと、ファイルのリムーバブルメディア特性が設定されているディスクデバイスオブジェクトに対してのみ、実行アクセスを許可し \_ \_ ます。 このため、リモートユーザーは、CD または DVD ドライブを使用してデータを書き込んだり、光学メディアにバックアップを実行したり、リムーバブルディスクをフォーマットしたりすることはできません。 管理者は、リムーバブル記憶域アクセスグループポリシーを設定して、既定の動作を上書きすることができます。 このポリシーが設定されている場合、i/o マネージャーは、これらのデバイスのリモートユーザーへのフルアクセスを許可して、読み取りおよび書き込み機能を許可します。

## <a name="span-idpnp_manager_and_removable_media_device_aclsspanspan-idpnp_manager_and_removable_media_device_aclsspanspan-idpnp_manager_and_removable_media_device_aclsspanpnp-manager-and-removable-media-device-acls"></a><span id="PnP_Manager_and_Removable_Media_Device_ACLs"></span><span id="pnp_manager_and_removable_media_device_acls"></span><span id="PNP_MANAGER_AND_REMOVABLE_MEDIA_DEVICE_ACLS"></span>PnP マネージャーとリムーバブルメディアデバイスの Acl


デバイスドライバースタックが開始されると、PnP マネージャーは、レジストリ内のデバイスのキーがそのデバイスのセキュリティ記述子を指定している場合にのみ、デバイスの ACL を変更します。 デバイスベンダーは、次のようにプロパティがに設定された**SetupDiSetDeviceRegistryProperty**を使用して、この記述子を設定できます。

**プロパティ**: spdrp \_ セキュリティ

**値**:**セキュリティ \_ 記述子**

**サイズ**: **sizeof**(セキュリティ \_ 記述子)


 

これらのプロパティは、ドライバーパッケージインストーラーを使用して設定することもできます。これを行うには、INF ファイルで関連するパラメーターを指定します。

## <a name="span-idgroup_policy_service_for_removable_storage_devices_aclsspanspan-idgroup_policy_service_for_removable_storage_devices_aclsspanspan-idgroup_policy_service_for_removable_storage_devices_aclsspangroup-policy-service-for-removable-storage-devices-acls"></a><span id="Group_Policy_Service_for_Removable_Storage_Devices_ACLs"></span><span id="group_policy_service_for_removable_storage_devices_acls"></span><span id="GROUP_POLICY_SERVICE_FOR_REMOVABLE_STORAGE_DEVICES_ACLS"></span>リムーバブル記憶装置のグループポリシーサービスの Acl


これは、管理者がディスクのボリュームインターフェイス、および CD または DVD 用のボリュームインターフェイス、テープとフロッピーディスクドライブ、およびグループポリシー framework を通じて WPD デバイスの Acl を設定できる Windows サービスです。 このグループポリシーは動的に変更できます。 ポリシーがコンピューターに適用されると、サービスはデバイスの ACL を更新します。 このサービスによって適用される ACL は、i/o マネージャーおよび PnP マネージャーによって設定された既定の ACL よりも優先されます。

グループポリシーサービスは、ディスクのボリュームインターフェイスに ACL を設定しますが、ディスククラスドライバーによって提供されるインターフェイスでは設定しません。 これは、アプリケーションがボリューム上のファイルとディレクトリにアクセスするときに、i/o マネージャーが対応するボリュームオブジェクトの ACL を使用して、呼び出し元に必要なアクセス許可があるかどうかを判断するためです。 そのため、ボリュームデバイスオブジェクトの ACL を設定することによって、グループポリシーサービスによって、そのボリュームに対して管理者が設定したアクセス権が適用されます。

## <a name="span-idsecurity_check_processspanspan-idsecurity_check_processspanspan-idsecurity_check_processspansecurity-check-process"></a><span id="Security_Check_Process"></span><span id="security_check_process"></span><span id="SECURITY_CHECK_PROCESS"></span>セキュリティチェックプロセス


アプリケーションがデバイスインターフェイスへのハンドルを開こうとすると、i/o マネージャーは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)呼び出しで要求されたアクセス許可がユーザーに付与されているかどうかを確認します。 Yes の場合、ハンドルが開かれます。そうしないと、呼び出しは失敗し、エラーアクセスが \_ 拒否されます。

ハンドルが開かれた後、アプリケーションは通常、IOCTL を使用して、デバイスに直接コマンドを送信できます。 たとえば、SCSI パススルーコマンドを送信する場合、アプリケーションは Ioctl scsi パススルーまた**は \_ \_ \_ ** **ioctl \_ scsi \_ パススルー \_ \_ **を使用します。

-   **IOCTL \_ディスク \_ 取得 \_ パーティション \_ 情報**には読み取りアクセスだけが必要です。

-   **IOCTL \_SCSI \_ パススルー \_ **と**IOCTL scsi パススルーを \_ \_ \_ \_ 直接実行**するには、呼び出し元が (ストレージデバイスドライバーによって提供される) インターフェイスへのハンドルを読み取りと書き込みの両方のアクセス用に開いている必要があります。

SCSI パススルー要求で指定されているコマンド記述子ブロック (CDB) のオペコードは、読み取り、書き込み、または読み取りと書き込みの両方のアクセス権が必要かどうかを判断するためにチェックされません。 このため、Windows では、アプリケーションが読み取り、書き込み、またはデータ転送をまったく行わない場合でも、パススルー要求の読み取りと書き込みのために、デバイスへのハンドルを常に開く必要があります。

**IOCTL \_\_** [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)呼び出しで要求されたアクセス許可に関係なく、ディスク確認を送信できます。 I/o マネージャーは IOCTL を受け取ると、その IOCTL に必要なアクセス許可をチェックし、 **CreateFile**呼び出しの呼び出し元に付与されたアクセス許可と比較します。 一致するものがある場合、IOCTL はターゲットデバイスに送信されます。それ以外の場合、IOCTL 呼び出しは失敗し、"アクセスが拒否されました" というエラーが発生し \_ ます。

たとえば、呼び出し元が読み取り専用アクセスのハンドルを開いている場合は、次のようになります。

-   **IOCTL \_SCSI \_ パススルー \_ **は、読み取りと書き込みの両方のアクセスを必要とするため、エラーアクセスが拒否されて失敗し \_ ます。

-   **IOCTL \_ディスクの \_ 取得 \_ パーティション \_ 情報**は、読み取りアクセスのみが必要なため、ドライバースタックに送信されます。

 

 




