---
title: ストレージ デバイス スタック、ストレージ ボリューム、ファイル システム スタック
description: ストレージ デバイス スタック、ストレージ ボリューム、ファイル システム スタック
ms.assetid: 5240ce9b-acfa-4e9c-9962-bc776878827c
keywords:
- 記憶装置 WDK ファイルシステム
- スタック WDK ファイルシステム
- デバイスオブジェクト WDK ファイルシステム
- ボリューム WDK ファイルシステム
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: bd36ca6cbb6eec8f6359da9c1413c7993566e441
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910469"
---
# <a name="storage-device-stacks-storage-volumes-and-file-system-stacks"></a>ストレージ デバイス スタック、ストレージ ボリューム、ファイル システム スタック

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

ファイルシステムのレガシフィルタードライバーがファイルシステムとボリュームにどのようにアタッチされるかを調べる前に、記憶域デバイススタック、記憶域ボリューム、およびファイルシステムスタック間の関係を理解する必要があります。

## <a name="storage-device-stacks"></a>ストレージ デバイス スタック

ほとんどの記憶装置ドライバーは pnp デバイスドライバーであり、PnP マネージャーによって読み込まれて管理されます。 記憶装置は、コンピューター上の物理デバイスまたは論理デバイスごとに、デバイスノード ( *devnode*) を含む PnP*デバイスツリー*で表されます。 ファイルシステムとファイルシステムフィルタードライバーは PnP デバイスドライバーではないことに注意してください。そのため、PnP[デバイスツリー]((https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree))にはそれらの devnodes が含まれていません。

特定の記憶装置の devnode には、デバイスの*記憶装置スタック*が含まれます。これは、デバイスの記憶装置ドライバーを表す、アタッチされたデバイスオブジェクトのチェーンです。 記憶域デバイス (ディスクなど) には論理ボリューム (パーティションまたはダイナミックボリューム) が1つ以上含まれている場合があるため、多くの場合、記憶域デバイススタック自体はスタックよりもツリーのように見えます。 このツリーのルートは、記憶域アダプターまたは記憶域スタックと統合されている別のデバイススタックの機能デバイスオブジェクト (FDO) です。 このツリーのリーフは、ファイルシステムボリュームをマウントできる論理ボリューム (*記憶域ボリューム*とも呼ばれます) の物理デバイスオブジェクト (pdos) です。

一般的な記憶装置スタックの図と説明については、「記憶装置設計ガイド」の次のセクションを参照してください。

- [SCSI HBA のデバイスオブジェクトの例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-scsi-hba)

- [IEEE 1394 コントローラーのデバイスオブジェクトの例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-an-ieee-1394-controller)

## <a name="storage-volumes"></a>ストレージ ボリューム

*ボリューム*は、記憶装置 (固定ディスク、フロッピーディスク、cd-rom など) で、ディレクトリとファイルを格納するようにフォーマットされています。 大きなボリュームは、*パーティション*とも呼ばれる複数の*論理ボリューム*に分けることができます。 各論理ボリュームは、NTFS、FAT、CDFS など、特定のメディアベースのファイルシステムで使用するようにフォーマットされています。

*記憶域ボリューム*(*記憶装置オブジェクト*) は、システムの論理ボリュームを表す、デバイスオブジェクト (通常は物理デバイスオブジェクト (PDO)) です。 ストレージデバイスオブジェクトは記憶装置スタックに存在しますが、必ずしもスタック内の最上位のデバイスオブジェクトであるとは限りません。

ファイルシステムが記憶域ボリュームにマウントされると、ファイルシステムのボリュームを表すファイルシステムボリュームデバイスオブジェクト (VDO) が作成されます。 ファイルシステム VDO は、*ボリュームパラメーターブロック*(vpb) と呼ばれる共有オブジェクトを使って、ストレージデバイスオブジェクトにマウントされます。

### <a name="mount-manager"></a>マウントマネージャー

*マウントマネージャー*は、ボリューム名、ドライブ文字、ボリュームマウントポイントなどの記憶域ボリューム情報の管理を行う i/o システムの一部です。 新しい記憶域ボリュームがシステムに追加されると、次のいずれかの方法でマウントマネージャーに到着が通知されます。

- ストレージボリュームを作成したクラスドライバーは、MOUNTDEV_MOUNTED_DEVICE_GUID インターフェイスクラスに新しいインターフェイスを登録するために[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出します。 これが発生すると、プラグアンドプレイデバイスインターフェイスの通知メカニズムによって、マウントマネージャーに対してシステムでのボリュームの到着が通知されます。

- 記憶域ボリュームのドライバーは、マウントマネージャーに IRP_MJ_DEVICE_CONTROL 要求を送信して、i/o 制御コードの[**IOCTL_MOUNTMGR_VOLUME_ARRIVAL_NOTIFICATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountmgr/ni-mountmgr-ioctl_mountmgr_volume_arrival_notification)を指定します。 この要求は、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出すことによって作成できます。

### <a name="unique-volume-name"></a>一意のボリューム名

マウントマネージャーは、ボリュームドライバーに次の情報を照会することによって、新しい記憶域ボリュームの到着に応答します。

- システムオブジェクトツリーの**デバイス**ディレクトリにある、ボリュームの非永続的なデバイスオブジェクト名 (またはターゲット名) (例: "\Device\HarddiskVolume1")

- ボリュームのグローバル一意識別子 (GUID)。*一意のボリューム名*とも呼ばれます。

- ドライブ文字など、ボリュームに対して推奨される永続的なシンボリックリンク名 (たとえば、"\ dosdevic%")

ストレージドライバーとマウントマネージャーの相互作用の詳細については、「[記憶域クラスドライバーでのマウントマネージャー要求のサポート](https://docs.microsoft.com/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver)」を参照してください。

## <a name="file-system-stacks"></a>ファイル システム スタック

ファイルシステムドライバーは、コントロールデバイスオブジェクト (CDO) とボリュームデバイスオブジェクト (VDO) という2種類のデバイスオブジェクトを作成します。 *ファイルシステムスタック*は、これらのデバイスオブジェクトの1つと、それにアタッチされているファイルシステムフィルタードライバーのすべてのフィルターデバイスオブジェクトで構成されます。 ファイルシステムのデバイスオブジェクトは、常にスタックの一番下を形成します。

### <a name="file-system-cdos"></a>ファイルシステム CDOs

ファイルシステムの CDOs は、個々のボリュームではなく、ファイルシステム全体を表し、グローバルファイルシステムキューに格納されます。 ファイルシステムによって、 **Driverentry**ルーチンに1つ以上の名前付き cdos が作成されます。 たとえば、FastFat は2つの CDOs を作成します。1つは固定メディア用で、もう1つはリムーバブルメディア用です。 CDFS は、リムーバブルメディアしかないため、CDO を1つだけ作成します。

ファイルシステムの CDOs には名前を付ける必要があります。 これは、ファイルシステムフィルタードライバーと多くのカーネルモードサポートルーチンが、それらを区別する手段として、VDOs と CDOs の違いに依存しているためです。

### <a name="file-system-vdos"></a>ファイルシステム VDOs

ファイルシステム VDOs は、ファイルシステムによってマウントされたボリュームを表します。 ファイルシステムはボリュームをマウントするときに VDO を作成し、通常はボリュームマウント要求に応答します。 CDO とは異なり、VDO は常に特定の論理または物理記憶装置に関連付けられています。

> [!NOTE]
> CDOs とは異なり、VDOs に名前を付けることはできません。これは、ボリュームデバイスオブジェクトに名前を付けるとセキュリティホールが作成されるためです。
