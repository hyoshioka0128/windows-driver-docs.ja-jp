---
title: 記憶域クラス ドライバーでのマウント マネージャーのサポート
description: 記憶域クラス ドライバーでのマウント マネージャーのサポート
ms.assetid: fb37f862-70d6-4514-b481-16f664346422
keywords:
- ストレージクラスドライバー WDK、マウントマネージャー
- クラスドライバー WDK storage、マウントマネージャー
- マウントマネージャー WDK ストレージ
- MM WDK ストレージ
- ボリューム名 WDK ストレージ
- WDK 記憶域の名前
- 一意のボリューム名 WDK ストレージ
- 永続的な名前データベース WDK ストレージ
- MountedDevices
- マウントされていないデバイスの WDK 記憶域
- シンボリックリンク名 WDK ストレージ
- 非永続的名 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a8b601638fe59e4b89f80f75539dbdf7ff5776
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844471"
---
# <a name="supporting-mount-manager-requests-in-a-storage-class-driver"></a>記憶域クラス ドライバーでのマウント マネージャーのサポート


## <span id="ddk_supporting_mount_manager_requests_in_a_storage_class_driver_kg"></span><span id="DDK_SUPPORTING_MOUNT_MANAGER_REQUESTS_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


マウントマネージャー (MM) は、ボリューム名の管理を担当します。 ボリュームごとに一意の名前が格納され、ボリュームがシステムから削除された後でも、ボリュームで完全に識別されます。 また、再起動によって保持される、ドライブ文字などの永続的ではない名前も管理しますが、システムにボリュームを追加したり、システムから削除したりすると、割り当てが変わる可能性があります。

マウントマネージャーは、ボリュームのデバイスオブジェクトへのシンボリックリンクを作成することによって、システム内の各ボリュームに固有のインターフェイスを提供します。 シンボリックリンク自体と対象となるデバイスオブジェクトは、システムの再起動時には保持されないため、マウントマネージャーは、シンボリックリンクの*名前*を*永続的な名前のデータベース*でレジストリに保持します。

このシンボリックリンク名は、*一意のボリューム名*と呼ばれます。 従来のボリュームラベルと同様に、システムの再起動時にも保持されますが、ドライブ文字と同様に、ボリュームラベルとは異なります。 一意のボリューム名の形式は次のとおりです。

" **\\?\\ボリューム {** <em>GUID</em> **}\\**

ここで、 *GUID*はボリュームを識別するグローバル一意識別子です。

マウントマネージャーの永続名データベースは、レジストリのシステムハイブ (**HKLM/SYSTEM/MountedDevices**) の**MountedDevices**レジストリキーにあります。 マウントマネージャーでは、一意のボリューム名に加えて、*マウントポイント*名も永続的な名前のデータベースに保存されます。 マウントポイント名は、さらに2つのカテゴリに分けることができます。これは、マウントされたボリュームのファイルシステムのルートディレクトリとして機能する Win32 形式のパス名とドライブ文字です。

データベース内の各永続シンボリックリンク名は、*一意の ID*を伴う**MountedDevices**キーの下に、レジストリ値の名前として表示されます。 一意の ID は、ボリュームの別の一意の識別子です (一意のボリューム名とは異なります)。 これは、同じボリュームを参照している可能性がある、多くの永続的なシンボリックリンク名を識別するのに役立ちます。

たとえば、ボリューム名が "\\\\のボリュームが1つあるとし<strong>ます。\\ボリューム {</strong>7603f260-142a-11d4-ac67-806d6172696f **}\\"** には、ドライブ文字"\\Dosdevices\\D: "と2つのマウントポイントがあります。\\Dosdevices\\C:\\mymount" および "\\DosDevices\\E:\\FilesysD\\mnt "です。 これにより、マウントマネージャーの永続的なシンボリックリンク名データベースに、一意のボリューム名、ドライブ文字用、2つのマウントポイント名用の2つのエントリが生成されます。 4つのエントリはすべて、同じ一意の id を共有します。したがって、 **MountedDevices**レジストリキーを表示すると、4つの永続的な名前がすべて同じボリュームを指していることを検出できます。

次の例は、 **MountedDevices**レジストリキーに永続的な名前がどのように表示されるかを示しています。

![mounteddevices レジストリキーに永続的な名前がどのように表示されるかを示すスクリーンショット](images/mntmgr.png)

マウントマネージャーは、プラグアンドプレイデバイスインターフェイスの通知メカニズムを利用して、ボリュームの到着と削除をアラートします。 したがって、すべてのクライアント (つまり、通常はクラスドライバー) は、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出してマウントマネージャーに通知することで、MOUNTDEV\_\_マウントされたデバイス\_GUID インターフェイスクラスにインターフェイスを作成する必要があります。it が管理するボリュームのシステムへの到達。 \_デバイス\_の\_マウントされた GUID インターフェイスクラス GUID は、 *mountmgr*で定義されています。

マウントマネージャーは、ボリュームインターフェイスが到着したプラグアンドプレイ通知を受け取ると、次の3つのデバイス制御 Irp をクライアントに送信します。

* [**IOCTL\_MOUNTDEV\_クエリ\_デバイス\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)
* [**IOCTL\_MOUNTDEV\_クエリ\_一意の\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_unique_id)
* [**IOCTL\_MOUNTDEV\_クエリ\_推奨される\_リンク\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)

これら3つの Ioctl に応答して、クライアントは、システムオブジェクトツリーの**デバイス**ディレクトリ (例: "\\Device\\HarddiskVolume1") にあるボリュームの非永続的デバイスオブジェクト名 (またはターゲット名) を返します。ボリューム ID と、推奨されるボリュームの永続的なシンボリックリンク名。 クライアントは Ioctl\_MOUNTDEV を無視するように選択することもできますが[ **\_クエリ\_提案された\_リンク\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)の場合は、 [**ioctl\_MOUNTDEV\_クエリの受信時に一意のボリューム ID を指定する必要があり\_デバイス\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)または IOCTL\_MOUNTDEV\_クエリ\_一意の\_ID。 マウントマネージャーは、一意のボリューム ID を提供するために、クライアントに完全に依存しています。クライアントが提供していない場合、マウントマネージャーはドライブ文字などのマウントポイントをボリュームに割り当てることができません。

これらの Ioctl の詳細については、「 [Mount Manager によって送信される I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

クライアントがボリュームの到着をマウントマネージャーに通知したが、照会されたときにボリュームの一意の ID を提供できない場合、ボリュームはマウントされていない*デバイス*の一覧に配置されます。 この場合、クライアントは[**ioctl\_\_\_MOUNTMGR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_check_unprocessed_volumes)を送信して、未処理の\_ボリューム ioctl をマウントマネージャーに送信して、マウントマネージャーがマウントされていないデバイスの一覧を再スキャンし、別のクエリを実行しようとするように要求することができます。一覧に表示されているクライアントは、それぞれのボリュームの一意の Id を示します。 IOCTL\_MOUNTMGR\_xxx Ioctl の詳細については、「 [Mount Manager クライアントによって送信される I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

マウントマネージャーは、新しく導入されたボリュームの一意のボリューム ID を受信した後、その一意の ID に割り当てられたすべての永続的な名前をそのデータベースで検索し、各固定シンボリックリンク名のボリュームへのシンボリックリンクを作成します。

ボリュームがオフラインになったことをマウントマネージャーが検出すると、そのデバイスオブジェクトを指すシンボリックリンクが削除されます。その際、マウントマネージャーのデータベース内の対応するシンボリックリンク名は削除されません。

マウントマネージャークライアントが永続的なシンボリック名を作成する方法の詳細については、「 [**IOCTL\_MOUNTMGR\_create\_POINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_create_point)」を参照してください。

 

 




