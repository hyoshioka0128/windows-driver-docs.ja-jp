---
title: ストレージ ボリューム
description: ストレージ ボリューム
ms.assetid: 37b65bb6-7c62-47be-a16d-3813dc4c1259
keywords:
- フィルター ドライバー WDK ファイル システム、記憶域ボリューム
- ファイル システム フィルター ドライバー WDK、記憶域ボリューム
- WDK の記憶域ボリューム ファイル システム
- マウント マネージャ WDK ファイル システム
- 記憶域デバイス オブジェクトの WDK ファイル システム
- WDK のボリュームのファイル システム、パラメーター ブロック
- Vpb WDK ファイル システム
- WDK のボリュームはファイル システム、記憶域ボリュームについて
- WDK の論理ボリューム ファイル システム
- WDK のパーティション ファイル システム
- 一意のボリューム名 WDK ファイル システム
- WDK の Guid はファイル システム
- WDK の名前のファイル システム
- 一意のボリューム名
- 使用中のステージング領域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33aa59f884e99a17349c2c73a66dd404553de677
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572954"
---
# <a name="storage-volumes"></a>ストレージ ボリューム


## <span id="ddk_storage_volumes_if"></span><span id="DDK_STORAGE_VOLUMES_IF"></span>


A*ボリューム*容量固定ディスク、フロッピー ディスク、CD-ROM、ディレクトリとファイルを格納する書式指定などのストレージ デバイスします。 大容量のボリュームを 1 つ以上に分割できます*論理ボリューム*も呼ばれ、*パーティション*します。 各論理ボリュームは NTFS、FAT、または CDFS など、特定のメディア ベースのファイル システムで使用する書式設定します。

A*記憶域ボリューム*、または*ストレージ デバイス オブジェクト*、通常、システムの論理ボリュームを表す物理デバイス オブジェクト (PDO) − − デバイス オブジェクトは、します。 記憶域デバイス オブジェクトは、記憶域デバイス スタックに存在するが、必ずしもがスタックの最上位のデバイス オブジェクトになることはありません。

記憶域ボリュームにファイル システムをマウントすると、ファイル システム ボリューム デバイス オブジェクトをファイル システム ボリュームを表すためには、(提供) が作成されます。 という名前の共有オブジェクトを使用して、記憶域デバイス オブジェクトに提供がマウントされているファイル システム、*ボリューム パラメーター ブロック*(VPB)。

### <a name="span-idddkmountmanagerifspanspan-idddkmountmanagerifspanmount-manager"></a><span id="ddk_mount_manager_if"></span><span id="DDK_MOUNT_MANAGER_IF"></span>マウント マネージャ

*マウント マネージャ*ボリューム名、ドライブ文字、およびボリュームのマウント ポイントの記憶域ボリュームの情報を管理を担当する I/O システムの一部です。 新しい記憶域ボリュームがシステムに追加されると、マウント マネージャは、次の方法のいずれかで到着の通知します。

-   記憶域ボリュームの呼び出しを作成するクラス ドライバー [ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506) 、MOUNTDEV で新しいインターフェイスを登録する\_マウント済み\_デバイス\_インターフェイス クラスの GUID です。 この場合、プラグ アンド プレイ デバイスのインターフェイスの通知メカニズムは、システムのボリュームの到着のマウント マネージャを警告します。

-   記憶域ボリューム用のドライバーが IRP マウント Manager に送信\_MJ\_デバイス\_制御の要求を指定する[ **IOCTL\_MOUNTMGR\_ボリューム\_到着\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff560477) I/O に対してコードを制御します。 この要求を呼び出すことによって作成できます[ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)します。

### <a name="span-idddkuniquevolumenameifspanspan-idddkuniquevolumenameifspanunique-volume-name"></a><span id="ddk_unique_volume_name_if"></span><span id="DDK_UNIQUE_VOLUME_NAME_IF"></span>一意のボリューム名

マウント マネージャは、ボリューム ドライバーについては、次のクエリを実行して、新しい記憶域ボリュームの着信に応答します。

-   ボリュームの非永続的デバイス オブジェクト名 (またはターゲット名) にある、**デバイス**システム オブジェクトのツリーのディレクトリ (例。"\\デバイス\\HarddiskVolume1")

-   ボリュームのグローバル一意識別子 (GUID) とも呼ばれる、*固有のボリューム名*

-   ドライブ文字など、ボリュームの推奨される永続的なシンボリック リンクの名前 (たとえば、"\\\dosdevices\z\\d:")

記憶装置ドライバーとマウント マネージャ間の相互作用の詳細については、[マウント マネージャーの要求、記憶域クラス ドライバーをサポートしている](https://msdn.microsoft.com/library/windows/hardware/ff567603)を参照してください。

 

 




