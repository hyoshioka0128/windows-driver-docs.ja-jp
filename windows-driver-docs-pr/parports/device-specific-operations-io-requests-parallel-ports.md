---
title: パラレル ポートの I/O 要求に対するデバイス固有の操作
description: パラレル ポートの I/O 要求の操作をデバイスに固有のドキュメントします。
keywords:
- WDK のパラレル ポート
- 並列ドライバー WDK
- 並列 IRP コード
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 38634b4c51f2009d3ca6ab7833a44296fa146248
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376960"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-ports"></a>パラレル ポートの I/O 要求に対するデバイス固有の操作
このトピックでは、パラレル ポートの I/O 要求の次のデバイスに固有の操作を説明します。

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)


##  <a name="irpmjcreate"></a>IRP_MJ_CREATE 
[Irp_mj_create 用](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求は、パラレル ポートを開きます。

### <a name="when-sent"></a>送信時
クライアントを使用する必要があります、 [irp_mj_create 用](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)ポートまたはデバイスにアクセスできる前に、パラレル ポートを開く要求をポートに接続します。

### <a name="input-parameters"></a>入力パラメーター
なし。

### <a name="output-parameters"></a>出力パラメーター
なし。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーが 0 に設定されます。

**状態**メンバーは、次の値のいずれかに設定されます。


STATUS_SUCCESS
 
パラレル ポートが正常に開きました。

STATUS_DELETE_PENDING 

デバイスは、プラグ アンド プレイ マネージャーによって削除される予定です。

### <a name="operation"></a>操作
パラレル ポートは、共有デバイスです。 パラレル ポートのシステムによって提供される関数のドライバーでは、パラレル ポートを開く要求を受信、単にパラレル ポートの開いているファイルの数を増やします。


##   <a name="irpmjinternaldevicecontrol"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求は、パラレル ポートの内部の動作モードを設定します。

### <a name="when-sent"></a>送信時
クライアントは、次の種類の操作を実行する内部デバイス コントロール要求を送信します。

* ポートに関する情報を取得します。
* ポートを割り当てるか、ポート上のデバイスを選択します
* 通信モードを設定します。

参照してください[パラレル ポートの内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

### <a name="input-parameters"></a>入力パラメーター
入力は、要求ごとに固有です。

### <a name="output-parameters"></a>出力パラメーター
出力は、要求ごとに固有です。

### <a name="io-status-block"></a>I/O ステータス ブロック
情報メンバーは、要求ごとに固有です。 

要求固有の値または汎用的な状態の値は次のいずれかに状態のメンバーに設定します。


STATUS_SUCCESS 

要求が正常に完了します。

STATUS_CANCELLED 

要求が取り消されました。

STATUS_DELETE_PENDING 

ドライブは削除中です。

STATUS_INVALID_PARAMETER 

パラレル ポートのシステムによって提供される関数のドライバーは、要求をサポートしていません。

STATUS_PENDING 

保留中の要求です。

### <a name="operation"></a>操作
操作は、要求ごとに固有です。

## <a name="related-topics"></a>関連トピック

[パラレル ポートの内部デバイス制御の要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[パラレル ポートに接続されている並列のデバイスの動作](https://docs.microsoft.com/windows-hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

