---
title: パラレル ポートの I/O 要求に対するデバイス固有の操作
description: パラレルポートに対する i/o 要求に対するデバイス固有の操作をドキュメント化します。
keywords:
- パラレルポート WDK
- パラレルドライバー WDK
- パラレル IRP コード
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3653b4c4081ffbc8e0d415cd2df3dd3acdef7f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831483"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-ports"></a>パラレル ポートの I/O 要求に対するデバイス固有の操作
このトピックでは、パラレルポートの i/o 要求に対する次のデバイス固有の操作について説明します。

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)


## <a name="irp_mj_create"></a>IRP_MJ_CREATE
[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求によって、パラレルポートが開かれます。

### <a name="when-sent"></a>送信時
クライアントは、ポートまたはポートに接続されているデバイスにアクセスする前に、 [IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求を使用してパラレルポートを開く必要があります。

### <a name="input-parameters"></a>入力パラメーター
なし。

### <a name="output-parameters"></a>出力パラメーター
なし。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーが0に設定されています。

**Status**メンバーは、次のいずれかの値に設定されます。


STATUS_SUCCESS
 
パラレルポートが正常に開かれました。

STATUS_DELETE_PENDING 

デバイスはプラグアンドプレイマネージャーによって削除されています。

### <a name="operation"></a>操作
パラレルポートは共有デバイスです。 パラレルポートに対してシステム提供の関数ドライバーがオープン要求を受信すると、パラレルポートで開いているファイルの数がインクリメントされます。


## <a name="irp_mj_internal_device_control"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求は、パラレルポートで内部動作モードを設定します。

### <a name="when-sent"></a>送信時
クライアントは、次の種類の操作を実行するために、内部のデバイス制御要求を送信します。

* ポートに関する情報を取得する
* ポートを割り当てるか、ポートでデバイスを選択します。
* 通信モードの設定

「[パラレルポートに対する内部デバイス制御要求」を](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)参照してください。

### <a name="input-parameters"></a>入力パラメーター
入力は要求に固有です。

### <a name="output-parameters"></a>出力パラメーター
出力は、要求に固有のものです。

### <a name="io-status-block"></a>I/O ステータス ブロック
情報メンバーは、要求に固有です。 

Status メンバーは、要求固有の値、または次の一般的な状態の値のいずれかに設定されます。


STATUS_SUCCESS 

要求は正常に完了しました。

STATUS_CANCELLED 

要求は取り消されました。

STATUS_DELETE_PENDING 

ドライブが削除されています。

STATUS_INVALID_PARAMETER 

並列ポート用のシステム提供の関数ドライバーは、要求をサポートしていません。

あります 

要求は保留中です。

### <a name="operation"></a>操作
操作は、要求に固有です。

## <a name="related-topics"></a>関連トピック

[パラレルポートに対する内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[パラレルポートに接続されているパラレルデバイスの操作](https://docs.microsoft.com/windows-hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

