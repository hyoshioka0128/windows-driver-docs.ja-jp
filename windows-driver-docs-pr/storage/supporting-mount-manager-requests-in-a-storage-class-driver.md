---
title: 記憶域クラス ドライバーでのマウント マネージャーのサポート
description: 記憶域クラス ドライバーでのマウント マネージャーのサポート
ms.assetid: fb37f862-70d6-4514-b481-16f664346422
keywords:
- 記憶域クラス ドライバー WDK、マウント マネージャ
- クラスのドライバー WDK の記憶域、マウント マネージャ
- WDK の記憶域をマウント マネージャ
- MM WDK ストレージ
- ボリューム名 WDK ストレージ
- 名前の WDK ストレージ
- 一意のボリューム名 WDK ストレージ
- 永続的な名前のデータベース ストレージの WDK
- MountedDevices
- デバイスの配信不能マウント WDK ストレージ
- シンボリック リンク名 WDK ストレージ
- 非永続的名 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a2c7d087294762a772aa848c7f1b4d8d483ef2b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368191"
---
# <a name="supporting-mount-manager-requests-in-a-storage-class-driver"></a>記憶域クラス ドライバーでのマウント マネージャーのサポート


## <span id="ddk_supporting_mount_manager_requests_in_a_storage_class_driver_kg"></span><span id="DDK_SUPPORTING_MOUNT_MANAGER_REQUESTS_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


マウント マネージャ (MM) は、ボリューム名を管理する責任を負います。 ボリュームごとに一意であり、ボリュームがシステムから削除された後も、そのボリュームには完全に識別する名前を格納します。 ドライブ文字は、再起動の前後で保持するが、割り当てを変更できますようにボリュームを追加またはシステムから削除のような小さい永続的な名前も管理します。

マウント マネージャは、ボリュームのデバイス オブジェクトへのシンボリック リンクを作成して、システム内の各ボリュームに固有のインターフェイスを提供します。 シンボリック リンク自体と、システムを再起動すると、対象にしているオブジェクトが保持されないデバイスの場合は、以降はマウント マネージャが保持されます、*名前*シンボリック リンクの*永続的な名前のデータベース*でレジストリ。

このシンボリック リンク名が呼び出される、*固有のボリューム名*します。 従来のボリューム ラベルのように、ボリューム ラベルとは異なりで一意であると、システムの再起動はなどのドライブ文字を保持します。 一意のボリューム名の形式です。

" **\\??\\ボリューム {** <em>GUID</em> **}\\**

場所*GUID*ボリュームを識別するグローバルに一意の識別子。

マウント マネージャの永続的な名前のデータベースにある、 **MountedDevices**システム ハイブのレジストリ キー (**HKLM/システム/MountedDevices**)、レジストリの。 マウント マネージャ、一意のボリューム名だけでなく格納も*マウント ポイント*その永続的な名前のデータベース内の名前。 マウント ポイント名は、さらに 2 つのカテゴリに分割できます。マウントされたボリュームのファイル システムのルート ディレクトリとして機能し、ドライブ文字を Win32 スタイル パス名。

下のレジストリ値の名前として、データベース内の各シンボリック リンクの永続的な名前が表示されます、 **MountedDevices**キーと共に、*一意の ID*します。 一意の ID は、(一意のボリューム名と異なる) ボリュームの別の一意の識別子です。 これにより、特定の可能性のある多数の永続的なシンボリック リンクの名前が同じボリュームを参照してください。

1 つのボリュームのボリュームの一意の名前を持つ、 <strong>"\\\\?\\ボリューム {0}</strong>7603f260-142a-11d4-ac67-806d6172696f **}\\"** 付属のドライブ文字があります"\\\dosdevices\z\\d:"と 2 つのマウント ポイント"\\\Dosdevices\z\\c:\\mymount"と"\\\dosdevices\z\\e:\\FilesysD\\mnt"。 これはマウント マネージャの永続的なシンボリック リンクのデータベースの名前で 4 つのエントリを生成します。 固有のボリュームのいずれか、ドライブ文字を 1 つずつ、2 つの名前、2 つのマウント ポイント名。 4 つすべてのエントリが同じ一意の id を共有します。表示するユーザーがそのため、 **MountedDevices**レジストリ キーは、同じボリュームの 4 つすべての永続的な名前を検出することになります。

次のスクリーン ショットは、どの永続的な名前を示しています。 で表示される、 **MountedDevices**レジストリ キー。

![スクリーン ショット mounteddevices のレジストリ キーに示すどの永続的な名前が表示されます。](images/mntmgr.png)

マウント マネージャは、そのボリュームの到着、削除のアラートを生成するプラグ アンド プレイ デバイス インターフェイス通知メカニズムに依存します。 (つまり、すべてのボリューム ドライバーが通常はクラス ドライバー) のすべてのクライアントが、MOUNTDEV でインターフェイスを作成する必要がありますので\_マウント済み\_デバイス\_GUID インターフェイスのクラスを呼び出して[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)の到着、管理対象のボリュームのシステムでのマウント マネージャを通知します。 MOUNTDEV\_マウント済み\_デバイス\_GUID インターフェイスのクラスで定義されている GUID *mountmgr.h*します。

ボリュームのインターフェイスの到着のプラグ アンド プレイの通知を受信するとマネージャー クライアントの 3 つのデバイス制御 Irp をマウントします。

* [**IOCTL\_MOUNTDEV\_クエリ\_デバイス\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)
* [**IOCTL\_MOUNTDEV\_クエリ\_UNIQUE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountdev/ni-mountdev-ioctl_mountdev_query_unique_id)
* [**IOCTL\_MOUNTDEV\_クエリ\_提案\_リンク\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)

これら 3 つの Ioctl への応答でクライアントが返されます、ボリュームのデバイスを非永続的オブジェクト名 (またはターゲット名) にあるで、**デバイス**システム オブジェクトのツリーのディレクトリ (例。"\\デバイス\\HarddiskVolume1")、ボリュームの一意の ID、および推奨される永続的なシンボリック リンクのそれぞれのボリュームの名前します。 クライアントは、無視することができますが[ **IOCTL\_MOUNTDEV\_クエリ\_提案\_リンク\_名前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)、する必要があります受信するとボリュームの一意の ID を指定[ **IOCTL\_MOUNTDEV\_クエリ\_デバイス\_名前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)または IOCTL\_MOUNTDEV\_クエリ\_UNIQUE\_id。 マウント マネージャが、一意のボリューム ID を指定するクライアントの完全に依存しています、クライアントを提供しないこと、しマウント マネージャでない場合、ドライブ文字など、マウント ポイントをボリュームに割り当てることができません。

これらの Ioctl の詳細については、次を参照してください。[マウント マネージャによって送信された I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

クライアントがそのボリュームの到着をマウント マネージャに警告が照会されたときに、ボリュームの一意の ID を提供できない場合は、ボリュームが掲載、*配信不能にマウントされているデバイス*一覧。 この場合、クライアントが送信できる、 [ **IOCTL\_MOUNTMGR\_確認\_UNPROCESSED\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountmgr/ni-mountmgr-ioctl_mountmgr_check_unprocessed_volumes) IOCTL マウント マネージャーに要求します。マウント マネージャはその配信不能にマウントされているデバイスの一覧を再スキャンして、それぞれのボリュームの一意の Id の一覧にクライアントを照会する別の試行です。 詳細については、IOCTL\_MOUNTMGR\_xxx Ioctl を参照してください[マウント Manager クライアントによって送信される I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

マウント後は、マネージャーは、新しく導入されたボリュームのボリュームの一意 ID を受け取ります。 次にその一意の ID に割り当てられている永続的な名前のすべてのデータベースを検索し、永続的なシンボリック リンク名ごとに、ボリュームへのシンボリック リンクを作成します。

ときにマウント マネージャはマウント マネージャのデータベースに対応するシンボリック リンク名を削除することがなく、デバイス オブジェクトを指すシンボリック リンクを削除し、ボリュームがオフラインなったことを検出します。

Mount manager のクライアントが永続的なシンボル名を作成する方法については、次を参照してください。 [ **IOCTL\_MOUNTMGR\_作成\_ポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountmgr/ni-mountmgr-ioctl_mountmgr_create_point)します。

 

 




