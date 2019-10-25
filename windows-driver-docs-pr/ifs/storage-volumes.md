---
title: ストレージ ボリューム
description: ストレージ ボリューム
ms.assetid: 37b65bb6-7c62-47be-a16d-3813dc4c1259
keywords:
- フィルタードライバー WDK ファイルシステム、記憶域ボリューム
- ファイルシステムフィルタードライバー WDK、ストレージボリューム
- 記憶域ボリューム WDK ファイルシステム
- マウントマネージャーの WDK ファイルシステム
- ストレージデバイスオブジェクト WDK ファイルシステム
- ボリューム WDK ファイルシステム、パラメーターブロック
- VPBs WDK ファイルシステム
- ボリューム WDK ファイルシステム、記憶域ボリュームについて
- 論理ボリューム WDK ファイルシステム
- WDK ファイルシステムのパーティション分割
- 一意のボリューム名 WDK ファイルシステム
- Guid WDK ファイルシステム
- WDK ファイルシステムの名前
- 一意のボリューム名
- ボリューム GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61831f5ac31a28c0eb85c64c5fe607511621a5a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840963"
---
# <a name="storage-volumes"></a>ストレージ ボリューム


## <span id="ddk_storage_volumes_if"></span><span id="DDK_STORAGE_VOLUMES_IF"></span>


*ボリューム*は、記憶装置 (固定ディスク、フロッピーディスク、cd-rom など) で、ディレクトリとファイルを格納するようにフォーマットされています。 大きなボリュームは、*パーティション*とも呼ばれる複数の*論理ボリューム*に分けることができます。 各論理ボリュームは、NTFS、FAT、CDFS など、特定のメディアベースのファイルシステムで使用するようにフォーマットされています。

*記憶域ボリューム*(*記憶装置オブジェクト*) は、システムの論理ボリュームを表す、デバイスオブジェクト (通常は物理デバイスオブジェクト (PDO)) です。 ストレージデバイスオブジェクトは記憶装置スタックに存在しますが、必ずしもスタック内の最上位のデバイスオブジェクトであるとは限りません。

ファイルシステムが記憶域ボリュームにマウントされると、ファイルシステムのボリュームを表すファイルシステムボリュームデバイスオブジェクト (VDO) が作成されます。 ファイルシステム VDO は、*ボリュームパラメーターブロック*(vpb) と呼ばれる共有オブジェクトを使って、ストレージデバイスオブジェクトにマウントされます。

### <a name="span-idddk_mount_manager_ifspanspan-idddk_mount_manager_ifspanmount-manager"></a><span id="ddk_mount_manager_if"></span><span id="DDK_MOUNT_MANAGER_IF"></span>マウントマネージャー

*マウントマネージャー*は、ボリューム名、ドライブ文字、ボリュームマウントポイントなどの記憶域ボリューム情報の管理を行う i/o システムの一部です。 新しいストレージボリュームがシステムに追加されると、次のいずれかの方法でマウントマネージャーに到着が通知されます。

-   ストレージボリュームを作成したクラスドライバーは、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出して、MOUNTDEV\_マウントされた\_デバイス\_GUID インターフェイスクラスに新しいインターフェイスを登録します。 これが発生すると、プラグアンドプレイデバイスインターフェイスの通知メカニズムによって、マウントマネージャーに対してシステムでのボリュームの到着が通知されます。

-   記憶域ボリュームのドライバーは、マウントマネージャーに対して、IRP\_MJ\_デバイス\_制御要求を送信します。これにより、i/o [ **\_MOUNTMGR\_ボリューム\_到着\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_volume_arrival_notification) i/o 制御コードの通知が指定されます。 この要求は、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出すことによって作成できます。

### <a name="span-idddk_unique_volume_name_ifspanspan-idddk_unique_volume_name_ifspanunique-volume-name"></a><span id="ddk_unique_volume_name_if"></span><span id="DDK_UNIQUE_VOLUME_NAME_IF"></span>一意のボリューム名

マウントマネージャーは、ボリュームドライバーに次の情報を照会することによって、新しい記憶域ボリュームの到着に応答します。

-   システムオブジェクトツリーの**デバイス**ディレクトリにある、ボリュームの非永続的なデバイスオブジェクト名 (またはターゲット名) (例: "\\Device\\HarddiskVolume1")

-   ボリュームのグローバル一意識別子 (GUID)。*一意のボリューム名*とも呼ばれます。

-   ドライブ文字など、ボリュームに対して推奨される永続的なシンボリックリンク名 (たとえば、"\\DosDevices\\D:")

ストレージドライバーとマウントマネージャーの相互作用の詳細については、「[記憶域クラスドライバーでのマウントマネージャー要求のサポート](https://docs.microsoft.com/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver)」を参照してください。

 

 




